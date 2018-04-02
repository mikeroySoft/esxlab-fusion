<!--
net_config/net-dns_config.md
-->

## Network DNS

Here's our network naming layout:

My Host networking is on the 10.0.1.0/24 network (physical.) This is my WiFi network the iMac is on. DNS services are running [in an Ubuntu VM](./dns-build.md) that is on Bridged network, and the vCSA is assigned a static IP and the DNS server at .75.

Your network will be different and your config files should reflect that.


| Host  | Role  | FQDN | IP |
|---|---|---|---|
| dns  |  Nameserver | dns.esxlab.local | 10.0.10.75
|  vcsa |  vCenter 6.5 Server Appliance | vcsa.esxlab.local | 10.0.10.131
|  vhost1  |  ESXi 6.5 Virtual Host | vhost1.esxlab.local | 10.0.10.141
|  vhost2  |  ESXi 6.5 Virtual Host | vhost2.esxlab.local | 10.0.10.142
|  vhost3  |  ESXi 6.5 Virtual Host | vhost3.esxlab.local | 10.0.10.143


<br>

## In the DNS VM

*(I'm using ubuntu 16.04 for simplicity)*

1) Create the zone folder and the files for our custom config:

```sudo mkdir /etc/bind/zones ```

2) Create /etc/bind/zones/[esxlab.local.db](./bind/zones/esxlab.local.db)

```sudo nano /etc/bind/zones/esxlab.local.db``` and replace the IP scheme with your own

3) Create /etc/bind/zones/[10.0.10.in-addr.arpa](./bind/zones/10.0.10.in-addr.arpa), replace the IP scheme with your own.
- The filename should also reflect your IP scheme. For example, if you're using 192.168.1.0/24, your reverse lookup file would be 1.168.192.in-addr.arpa, and contain records for a 192.168.1.0 network.

```sudo nano /etc/bind/zones/10.0.10.in-addr.arpa``` 


4) Set the DNS nameserver in /etc/resolvconf/[resolv.conf.d/base](resolv.conf.d/base)

```$ sudo nano /etc/resolvconf/resolv.conf.d/base```


5) Now update resolvconf:

```$ sudo resolvconf -u```
