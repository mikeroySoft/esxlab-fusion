<!--
host_config/host-network.md
-->

# Host Networking

In order for the vCenter Server appliance .OVA to come up gracefully, we need to have certain network controls prepared and ready in advance

Specifically, we need to:
- Have multiple, isolated virtual networks for the various vSphere control layers
- Configure and manage DHCP
- DNS forward and reverse lookup for at least the vCSA and 1 host.
- Expose the VMs inside ESXi virtual hosts to the Internet (NAT)

For a proper nested lab setup we use Fusion to create the following Virtual networks: (Feel free to segment them as you desire, this is just a suggestion that works for me)


| Network  | Subnet  | NAT | Connect Mac | DHCP |
|---|---|---|:---:|---|
| vmnet2-mgmt  |  10.20.20.0/24 | No | Yes | Yes
|  vmnet3-storage |  10.20.30.0/24 | No | No | Yes
|  vmnet4-fault  |  10.20.40.0/24 | No | No | Yes
|  vmnet7-vmnet  | 192.168.70.0/24 | Yes | Yes | Yes

These are set up on the host using either the Fusion UI or by pasting [this file](../net_config/fusion_prefs/networking) over your /Library/Preferences/VMware Fusion/networking file.

If you're using the Fusion UI to set this up,
- Navigate to the Menu Bar > Vmware Fusion > Preferences > Networking
- Unlock to make changes
- Click the '+' button to add a new virtual network
- Configure the network according to the above table
- Repeat for each network required

Each virtual network also has options to configure DHCP, and this is recommended instead of using static IPs within vms directly.
The vmnet-specific configuration options are located in the resepctive 'vmnet' folder.

```bash
➜ ls -la /Library/Preferences/VMware\ Fusion
total 48
-r--r--r--   1 root  wheel    31 26 Mar 00:16 lastLocationUsed
-rw-r--r--   1 root  wheel   689 24 Feb 00:35 license-fusion-100-e4-201704
-rw-r--r--   1 root  wheel  1832  6 Jan 17:56 networking
-rw-r--r--   1 root  wheel  1418 22 Mar 00:43 networking.bak.0
drwxr-xr-x@ 10 root  wheel   320 26 Mar 00:16 thnuclnt
drwxr-xr-x   4 root  wheel   128 25 Feb 01:00 vmnet1
drwxr-xr-x   4 root  wheel   128 22 Mar 00:43 vmnet2
drwxr-xr-x   4 root  wheel   128 23 Mar 17:22 vmnet3
drwxr-xr-x   4 root  wheel   128 23 Mar 17:22 vmnet4
drwxr-xr-x   4 root  wheel   128 23 Mar 17:22 vmnet5
drwxr-xr-x   7 root  wheel   224 25 Feb 13:19 vmnet7
drwxr-xr-x   7 root  wheel   224 25 Feb 01:00 vmnet8
```

```bash
➜ ls -la /Library/Preferences/VMware\ Fusion/vmnet2
total 40
drwxr-xr-x   7 root  wheel   224 25 Feb 13:19 .
drwxr-xr-x  16 root  wheel   512 26 Mar 00:21 ..
-rw-r--r--   1 root  wheel  1673 23 Mar 17:22 dhcpd.conf
-rw-r--r--   1 root  wheel  1755 23 Mar 17:22 dhcpd.conf.bak
-rw-r--r--   1 root  wheel  1565 23 Mar 17:22 nat.conf
-rw-r--r--   1 root  wheel  1565 23 Mar 17:22 nat.conf.bak
-rw-r--r--   1 root  wheel    18 26 Mar 00:21 nat.mac
```

The `dhcpd.conf` file needs to be edited for vmnet2, but for the other vmnets we can keep them using the default dhcp scope.

Use the file [here](../net_config/fusion_prefs/vmnet2-dhcpd.conf) as a configuration example. Be sure to change the MAC addresses to reflect your VMs.

*Be sure to write below the 'DO NOT MODIFY' section or your config options will be overwritten.*

The format is essentially:

```
host [vHost1] {                             // Your VMs Hostname
	hardware ethernet 00:50:56:34:EA:DF;    // Your VMs MAC address
	fixed-address 10.20.20.41;              // The IP you want to give the VM
	option domain-name-servers 10.20.20.20; // DNS Server Address
	option domain-name "esxlab.local";      // local default lookup
}
```

Once we've configured DHCP on vmnet2 for the vhosts, dns server and the vCSA we can verify things work using the dns server.

## DNS Server Config

Before getting to the actual bind config, we need to make sure the DNS VM is connected to both the Management network as well as the VM network.
This is covered in the [dns-build.md guide](../net_config/dns-build.md)
The Management network is what we're using to get ESXi connected to the vCenter Server, but it should not have internet connectivity.
Our dns server needs updates from the web, and to potentially provide DNS services to VMs running in the nested lab, so we facilitate this by using 2 network adapters on the DNS virtual machine: One connected to vmnet2 and one to vmnet7.
