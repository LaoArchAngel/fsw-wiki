# Setting up HaProxy w/ Keepalived as a software loadbalancer

## Executive Summary

## Server Setup

### To start, you need to machines and a Virtual IP:

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

