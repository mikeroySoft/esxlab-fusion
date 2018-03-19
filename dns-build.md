sudo mkdir /etc/bind/zones
sudo nano /etc/bind/zones/esxlab.local.db
sudo nano /etc/bind/zones/rev.5.168.192.in-addr.arpa

mLab.local.db


named.conf.local

zone "esxlab.local" {
        type master;
        file "/etc/bind/zones/esxlab.local.db";
        };

# This is the zone definition for reverse DNS. replace 0.168.192 with your network address in reverse notation - e.g my network address is 192.168.0
zone "5.168.192.in-addr.arpa" {
     type master;
     file "/etc/bind/zones/rev.5.168.192.in-addr.arpa";
};


sudo mkdir /etc/bind/zones
sudo nano /etc/bind/zones/mlab.local.db
sudo nano /etc/bind/zones/rev.5.168.192.in-addr.arpa


esxlab.local.db

$TTL	86400 ; 24 hours could have been written as 24h or 1d
; $TTL used for all RRs without explicit TTL value
$ORIGIN esxlab.local.
@  1D  IN  SOA esxlabdns.esxlab.local. hostmaster.esxlab.local. (
			      2002022401 ; serial
			      3H ; refresh
			      15 ; retry
			      1w ; expire
			      3h ; minimum
			     )
esxlab.local.      IN      NS              esxlabdns.esxlab.local.


esxlabdns    IN  A      192.168.5.53
vcsa66       IN  A      192.168.5.19
esx6host1    IN  A      192.168.5.20
esx6host2    IN  A      192.168.5.21


rev.5.168.192.in-addr.arpa

@ IN SOA esxlabdns.esxlab.local. admin.esxlab.local. (
                        2006081401;
                        28800;
                        604800;
                        604800;
                        86400
)

           IN    NS     esxlabdns.esxlab.local.
53         IN    PTR    esxlab.local
19	   IN	 PTR	vcsa6
20	   IN	 PTR	esx6host1
21	   IN	 PTR	esx6host2


/etc/resolve.conf
search esxlab.local
nameserver 192.168.5.53
