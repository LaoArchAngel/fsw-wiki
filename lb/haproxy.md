# Setting up HaProxy w/ Keepalived as a software loadbalancer

## Executive Summary

## Server Setup

### To start, you need to define 2 load balancer machines and a Virtual IP:

    10.0.49.181 vip    
    10.0.49.179 server1
    10.0.49.180 server2

### Each machine requires haproxy:

    sudo yum install haproxy
    # edit /etc/haproxy/haproxy.cfg
    sudo setsebool -P haproxy_connect_any=1
    sudo firewall-cmd --permanent --add-port=1988/tcp
    sudo firewall-cmd --permanent --add-service=https
    sudo systemctl restart firewalld.service
    sudo systemctl restart haproxy
    sudo systemctl status haproxy -l


In order to load balance ssl traffic, the server will need one ssl certificate (dev in the example below).
First we need to create the certificate file with all the necessary pieces:

    cat dev-fsw.com.crt dev-fsw.com.key ca-bundle.crt > /etc/haproxy/dev-fsw.com.pem
    sudo chmod 600 /etc/haproxy/dev-fsw.com.pem
    sudo chown root:root /etc/haproxy/dev-fsw.com.pem

We also need to set the correct SELinux permissions:

    sudo chcon -u system_u /etc/haproxy/dev-fsw.com.pem
    sudo chcon -r object_r /etc/haproxy/dev-fsw.com.pem
    sudo chcon -t etc_t /etc/haproxy/dev-fsw.com.pem
    sudo ls -lZ /etc/haproxy/dev-fsw.com.pem


### Each machine requires keepalived:

    sudo yum install keepalived
    sudo systemctl enable keepalived
    sudo cp /etc/keepalived/keepalived.conf /etc/keepalived/keepalived.conf.bak
    sudo vi /etc/keepalived/keepalived.conf
    sudo systemctl start keepalived


-----------------------------------------------------------------------------------------------------------------


! Configuration File for keepalived on server1

```bash
global_defs {
	router_id server1 # hostname

	notification_email {
		support@fsw.com
	}
	notification_email_from server1@fsw.com
	smtp_server obm.foodservicewarehouse.com
	smtp_connect_timeout 30
}

vrrp_script check_haproxy {
	script "killall -0 haproxy"
	interval 2 # every 2 seconds
	weight 2 # add 2 points if OK
}

vrrp_instance VI_1 {
	state MASTER # MASTER on server1, BACKUP on server2
	interface eno16777984 # interface to monitor
	virtual_router_id 51
	priority 101 # 101 on server1, 100 on server2
	advert_int 1

	virtual_ipaddress {
		10.0.49.181 dev eno16777984 #virtual ip address
	}
	track_script {
		check_haproxy
	}
}

```

-----------------------------------------------------------------------------------------------------------------


! Configuration File for keepalived server2

```bash

global_defs {
	router_id devhaproxy02
	notification_email {
		jstorfa@fsw.com
	}
	notification_email_from devhaproxy02@fsw.com
	smtp_server obm.foodservicewarehouse.com
	smtp_connect_timeout 30
}

vrrp_script check_devhaproxy {
	script "killall -0 haproxy"
	interval 2 # every 2 seconds
	weight 2 # add 2 points if OK
}

vrrp_instance VI_1 {
	state BACKUP # MASTER on devhaproxy01, BACKUP on devhaproxy2
	interface eno16777984 # interface to monitor
	virtual_router_id 51
	priority 100 # 101 on devhaproxy01 and 100 on devhaproxy2
	advert_int 1

	virtual_ipaddress {
		10.0.49.181 dev eno16777984 # virtual ip address
	}
}

```

### Each machine requires an haproxy-cfg-api:

Clone the [node-haproxy-cfg-api](https://github.com/looking-promising/node-haproxy-cfg-api/tree/dev/no-thalassa) repo and checkout the `no-thalassa` branch.

```bash
git clone git@github.com:looking-promising/node-haproxy-cfg-api.git
git checkout no-thalassa
```

Then create a `data-persistence` directory and reference it when starting up the api server:

```bash
mkdir data-persistence
sudo bin/server.js --port 8080 --haproxyPidPath /run/haproxy.pid --haproxyCfgPath /etc/haproxy/haproxy.cfg --persistence ./data-persistence/data --sudo  --debug
```

## Use the REST API to configure haproxy

Create a default backend

```bash
curl -X PUT -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: eb57ad59-52fc-7194-4e08-4de1ac8f8343" -d '{
    "type": "static",
    "name": "default",
    "version": "1.0.0",
    "balance": "roundrobin",
    "mode": "http",
    "members": [
        {
            "name": "localhost",
            "version": "1.0.0",
            "host": "127.0.0.1",
            "port": 9000
        }    
    ]
}' "http://192.168.111.10:8080/backends/default"
```

Create a backend to a non-ssl app on non-standard port:

```bash
curl -X PUT -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: c27384f8-1f41-66e7-4d12-9d3d96a1e739" -d '{
    "type": "static",
    "name": "gator-live",
    "version": "1.0.0",
    "balance": "roundrobin",
    "mode": "http",
    "members": [
        {
            "name": "fswgator01",
            "version": "1.0.0",
            "host": "10.0.49.76",
            "port": 9000
        }    
    ]
}' "http://192.168.111.10:8080/backends/gator-live"
```

Create an ssl backend for the dev-fsw.com domain:

```bash
curl -X PUT -H "Content-Type: application/json" -H "Cache-Control: no-cache" -H "Postman-Token: 02423cca-dea2-a655-195c-64187c81b829" -d '
{
    "type": "static",
    "name": "authcentral-live",
    "balance": "roundrobin",
    "mode": "http",
    "members": [
       {
            "name": "fswauthdev01",
            "version": "1.0.0",
            "host": "10.0.50.226",
            "port": "443",
            "options": "ssl ca-file /etc/haproxy/dev-fsw.com.pem verify required weight 10 maxconn 100",
            "lastKnown": ""
        }
    ]
}' "http://192.168.111.10:8080/backends/authcentral-live"

```

Create the https frontend that routes traffic the correct backend based on host header:

```bash

{
    "key": "https",
    "bind": "*:443 ssl crt /etc/haproxy/dev-fsw.com.pem",
    "mode": "http",
    "keepalive": "server-close",
    "backend": "default",
    "rules": [
        {
          "type": "header",
          "header": "host",
          "operation": "hdr_dom",
          "value": "gator.dev-fsw.com",
          "backend": "gator-live"
        },
        {
          "type": "header",
          "header": "host",
          "operation": "hdr_dom",
          "value": "secure.dev-fsw.com",
          "backend": "authcentral-live"
        }
    ],
    "natives": []
}

```

The resulting haproxy config should look like this:

```bash

global
  log 127.0.0.1 local0
  log 127.0.0.1 local1 notice
  daemon
  maxconn 4096
  tune.ssl.default-dh-param 2048

  # stats socket /tmp/haproxy.status.sock user USER_RUNNING_NODE_PROCESS level admin
  stats socket /tmp/haproxy.status.sock level admin

  defaults
    log global
    option dontlognull
    option redispatch
    retries 3
    maxconn 2000
    timeout connect 5000ms
    timeout client 50000ms
    timeout server 50000ms

  listen stats :1988
    mode http
    stats enable
    stats uri /
    stats refresh 2s
    stats realm Haproxy\ Stats
    stats auth showme:showme

  frontend https
    option forwardfor
    http-request set-header X-Forwarded-Proto https if { ssl_fc }
    bind *:443 ssl crt /etc/haproxy/dev-fsw.com.pem
    mode http
    default_backend default
    option httplog
    option http-server-close
    option http-pretend-keepalive
    acl header_cc8fr hdr_dom(host) gator.dev-fsw.com
    use_backend gator-live if header_cc8fr
    acl header_vobt9 hdr_dom(host) secure.dev-fsw.com
    use_backend authcentral-live if header_vobt9

  backend authcentral-live
    mode http
    balance roundrobin
    server authcentral-live_10.0.50.226:443 10.0.50.226:443 ssl ca-file /etc/haproxy/dev-fsw.com.pem verify required weight 10 maxconn 100 check inter 2000

  backend default
    mode http
    balance roundrobin
    server default_127.0.0.1:9000 127.0.0.1:9000  check inter 2000

  backend gator-live
    mode http
    balance roundrobin
    server gator-live_10.0.49.76:9000 10.0.49.76:9000  check inter 2000

```

Now, assuming dns resolves to your VIP for the following domains, the load balancer should route traffic as follows:

```bash
https://gator.dev-fsw.com       --> http://10.0.49.76:9000
https://secure.dev-fsw.com      --> https://10.0.50.226:443
https://unavailable.dev-fsw.com --> returns a `503 Service Unavailable` result
```

And, as a final check, we can view the frontends and backends in the haproxy statistics UI:

![haproxy_statistics_report](/uploads/3db23e50c116c5871b3061a377c74564/haproxy_statistics_report.png)
