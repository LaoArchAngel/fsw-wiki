### list current firewall rules

```bash
sudo firewall-cmd --zone=public --list-all
```

### update firewall config and reload

```bash
sudo firewall-cmd --permanent --zone=public --add-port=<PORT>/tcp && sudo firewall-cmd –reload
```

### list the new firewall rules

```bash
sudo firewall-cmd --zone=public --list-all
```

### More Details: 
* http://www.tejasbarot.com/2014/08/05/rhel-7-centos-7-how-to-get-started-with-firewalld/#axzz3Y9DddtlX
* https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Security_Guide/sec-Using_Firewalls.html
