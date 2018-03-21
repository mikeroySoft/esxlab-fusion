## In DNS box (I'm using ubuntu 18.04):

*Netplan is the new default network system manager FYI*

sudo mkdir /etc/bind/zones
sudo nano /etc/bind/zones/esxlab.local.db
sudo nano /etc/bind/zones/20.20.10.in-addr.arpa
sudo nano /etc/systemd/resolved.conf

sudo nano 01-netcfg.yaml

sudo netplan apply

### On the Mac Host
cd /Library/Preferences/VMware\ Fusion
nano vmnet2/dhcpd.conf
