<!--
esxlab-quickstart.md
-->

## Overview
This repo contains a simplified demo configuration to build a 1-Host vSphere 6.5 U1 cluster using VMware Fusion 10.1.1

I have documented two paths: [Quick Start](./esxlab-quickstart.md) and [Full Lab](./esxlab-full_lab.md)

The full lab is still under construction, but our Quick Start guide is this document.


## Quick Start Guide

The goal of this configuration will be to have a simple vCenter Server running with 3 number of ESXi nodes, with very basic networking.

The overall process will be as follows:
- [**Set Up Host Networking**](./host_config/host-network_setup.md)
  - 5 VM Networks
    - *VM Traffic*
      - We will just use the built-in 'NAT' network for this (vmnet8)
    - *Management*
      - We will just use Bridged for the Management layer due to the vCSA not really liking it when you mess with networking before first-boot.


- [**Create and configure virtual host(s)**](./host_config/host-setup_vhosts.md)
  - remove unnecessary virtual hardware components (Camera, USB Adapter)
  - Configure Network Adapters
    - Configure existing NIC: Bridged(Autodetect)
    - Add 1 NIC: NAT


- [**Setup DNS**](./net_config/net-dns_config.md)
  - Forward and Reverse lookup for:
     - vCenter server (vCSA 6.5)
     - 3 virtual hosts (ESXi 6.5)
     - 1 DNS Server
  - DNS VM Bridged network


- [**Deploy the vCenter Server Appliance OVA**](./host_config/host-deploy_vcsa.md)
  - extract .ova file from .iso
  - file > new > import > .ova
  - vCSA configuration walkthrough built into Fusion
    - Fill out all required values


- [**Boot the vCSA**](./host_config/host-deploy_vcsa.md)
  - Wait until it looks finished, then wait 10 minutes


- [**Load the vCSA Host Web UI**](./host_config/host-config_vcsa.md)
  - Ensure everything is green, make any changes


- [**Load the vSphere Client (web ui)**](./mgmt_config/mgmt-config_vcsa.md)
  - Login with admin passwords used in OVA properties


- [**Build the vSphere lab**](./mgmt_config/mgmt-vsphere_lab_buildout.md)
  - Add esxlab-vHosts


- [**Add some VMs**](./lab_config/lab_setup-add_vms.md)

From here you should have a nice little 3-host vSphere cluster running. <br>
What remains is to:
  - Add 2 more virtual ESXi hosts
  - Set up storage networking
  - Set up storage clusters, vSAN
  - Add some VMs
