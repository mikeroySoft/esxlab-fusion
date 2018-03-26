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

The `dhcpd.conf` file needs to be edited for vmnet2, but for the other vmnets we can keep them using the default dhcp scope.

Walkthrough for configuring the dhcpd included with Fusion is [here](../net_config/net-dhcp_config.dm).


Once we've configured DHCP on vmnet2 for the vhosts, dns server and the vCSA we can verify things work using the dns server.

## DNS Server Config

Before getting to the actual bind config, we need to make sure the DNS VM is connected to both the Management network as well as the VM network.
This is covered in the [dns-build.md guide](../net_config/dns-build.md)
The Management network is what we're using to get ESXi connected to the vCenter Server, but it should not have internet connectivity.
Our dns server needs updates from the web, and to potentially provide DNS services to VMs running in the nested lab, so we facilitate this by using 2 network adapters on the DNS virtual machine: One connected to vmnet2 and one to vmnet7.
