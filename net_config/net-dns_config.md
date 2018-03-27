<!--
net_config/net-dns_config.md
-->

## In DNS box (I'm using ubuntu 17.04):

Here's our network naming layout:

| Host  | Role  | FQDN | IP |
|---|---|---|---|
| dns  |  Nameserver | dns.esxlab.local | 10.20.20.20
|  vcsa |  vCenter 6.5 Server Appliance | vcsa.esxlab.local | 10.20.20.31
|  vhost1  |  ESXi 6.5 Virtual Host | vhost1.esxlab.local | 10.20.20.41
|  vhost2  |  ESXi 6.5 Virtual Host | vhost2.esxlab.local | 10.20.20.42
|  vhost3  |  ESXi 6.5 Virtual Host | vhost3.esxlab.local | 10.20.20.43


<br>

Create the zone folder and the files for our custom config:

```sudo mkdir /etc/bind/zones ```

Create /etc/bind/zones/[esxlab.local.db](./bind/zones/esxlab.local.db)

```sudo nano /etc/bind/zones/esxlab.local.db```

And /etc/bind/zones/[20.20.10.in-addr.arpa](./bind/zones/20.20.10.in-addr.arpa)

```sudo nano /etc/bind/zones/20.20.10.in-addr.arpa```


Set the DNS nameserver in /etc/resolvconf/[resolv.conf.d/base](resolv.conf.d/base)

```$ sudo nano /etc/resolvconf/resolv.conf.d/base```


Now update resolvconf:

```$ sudo resolvconf -u```




### On the Mac Host
cd /Library/Preferences/VMware\ Fusion
nano vmnet2/dhcpd.conf
