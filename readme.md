# esxlab-fusion

Series of documents and config boilerplate to get a vSphere lab up and running quickly in VMware Fusion 10

## Overview
This repo contains a simplified demo configuration to build a Multi-Host vSphere 6.5 U1 cluster using VMware Fusion 10.1.1

I have documented two paths: [Quick Start](./esxlab-quickstart.md) and [Full Lab](./esxlab-full_lab.md)

The full lab is still under construction, but our Quick Start guide is [this document](./esxlab-quickstart.md).

### Prerequisites

The following are necessary to get this running:


- A sufficiently powerful Mac  
  - *I'm using an iMacPro1,1 10-CPU cores and 64GB of RAM, a MacBook Pro with 4 cores and 16GB of RAM will work but with much less ability to run nested VMs and larger nested data center designs. Could probably only really deploy the vCSA (minimum 2 CPU, 10GB/RAM) and perhaps 1 vHost.*
- VMware Fusion Pro version 10.1.1
  - Available at [vmware.com/go/getfusion](http://www.vmware.com/go/getfusion)
- ISO files for: (trial license keys will work)
  - [ESXi](https://my.vmware.com/group/vmware/details?downloadGroup=ESXI65U1&productId=614&rPId=21946)
  - [vCenter Server](https://my.vmware.com/group/vmware/details?downloadGroup=VC65U1G&productId=614&rPId=21946)
- DNS server
  - ([bind9](./net_config/net-dns_config.md) or Windows Domain Controller)


### Installing

To get started, use the quickstart guide located [here](./esxlab-quickstart.md).

Please feel free to submit issues and pull requests to help us improve =)
