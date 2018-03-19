# esxlab-fusion Introduction

## Overview
This repo contains instructions and demo configurations to build a 3-tier vSphere cluster using VMware Fusion 10.1.1

The overall process will be as follows:
- **Set Up Host Networking**
  - 5 VM Networks
    - *VM Traffic*
    - *Management*
    - *Storage (vSAN)*
    - *Fault Tolerance*
    - *vMotion*


- **Create and configure 1 virtual host**
  - remove unnecessary virtual hardware components
  - Add 4 NICs (5 total)
  - generate MAC addresses, capture them, add to dhcp tables


- **Full-Clone the Virtual Host** *(3 total vHosts in this design)*
  - Re-Generate MAC Addresses, capture them, add to dhcp tables


- **Create necessary DNS entries**
 - vCenter server
 - 3 virtual hosts
 - 1 DNS Server (tiny ubuntu 18.04 with bind)
 - 1 vSAN shared storage setup


- **Deploy the vCenter Server Appliance OVA**
 - extract .ova file from .iso
 - file > new > import > .ova
 - vCSA configuration walkthrough built into Fusion (do not boot yet)
 - Reconfigure the vCSA virtual hardware before booting for performance


- **Boot the vCSA**
  - Wait until it looks finished, then wait 10 minutes


- **Load the vCSA Host Web UI**
  - Ensure everything is green, make any changes


- **Load the vSphere Client (web ui)**
  - Login with admin passwords used in OVA properties


- **Build the vSphere lab**
  - Add esxlab-vHosts
  - Set up networking
  - Set up storage
  - Add some VMs


- *Bonus material: for extra points:*
  - Set up HA
  - Set up DRS
  - Perform a vMotion
  - Try PoweCLI
  - Try installing open source integrations
    - Harbor
    - Admiral
    - Flings
    - vSphere Integrated Containers
