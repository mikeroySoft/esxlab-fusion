<!--
host_config/esxlab-full_lab.md
-->
# esxlab-fusion Introduction

## Overview
This repo contains instructions and demo configurations to build a 3-tier vSphere cluster using VMware Fusion 10.1.1

I have documented two paths: [Quick Start](./esxlab-quickstart.md) and [Full Lab](./esxlab-full_lab.md)

The full lab is still under construction, but our Quick Start guide is [here](./esxlab-quickstart.md).


## Full Lab Guide

The overall process will be as follows:
- [**Set Up Host Networking**](./host_config/host-network_setup.md)
  - 5 Virtual Host Networks from Fusion Preferences > Network
    - *VM Traffic*
      - We will just use the built-in 'NAT' network for this (vmnet8)
    - *Management*
      - Initially we will just use Bridged for the Management layer due to the vCSA not really liking it when you mess with networking before first-boot. We will later transition to using vmnet2 for Management.
    - *Storage (vSAN)*
    - *Fault Tolerance*
    - *vMotion*


- [**Create and configure 3 virtual hosts**](./host_config/host-setup_vhosts.md)
  - remove unnecessary virtual hardware components
  - Add 4 NICs (5 total)
  - generate MAC addresses, capture them, add to dhcp scope


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

From here you should have a nice little 3-host vSphere cluster running. <br>
What remains is to:
  - Set up networking (storage, vmotion, drs, etc..)
  - Set up storage
  - Add some VMs

- *Bonus material: for extra points:*
  - Set up HA
  - Set up DRS
  - Perform a vMotion
  - Try PoweCLI
  - Try installing open source integrations
    - vSphere Integrated Containers
    - Harbor
    - Other Flings
