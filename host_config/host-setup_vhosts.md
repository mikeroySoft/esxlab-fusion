<!--
host-setup_vhosts.md
-->

## esxlab Virtual ESXi Host Setup

This document will guide you through configuring the ESXi Host you previously installed from [this document](./host-install_esx.md).

### Overview

Once the VM boots to the yellow ESXi console, you may need to log in and configure the IP and DNS information. In our lab we use a static IP and have a DNS entry for the host for convenience.

- Log into the Console with 'F2' (Use the 'Fn' button to toggle the function keys)
- Enter the root password you set up during the ESXi installation
- Select 'Configure Management Network'
- Select IP Configuration and press Enter.
- Select Set static IP address and network configuration.
- Enter the IP address, subnet mask, and default gateway and press Return / Enter

Once the host is up with an IP address that responds to ping (try ping vhost1.esxlab.local to verify dns is working), we can add it to our vCenter Server Appliance.

[Follow this document](../mgmt_config/mgmt-vsphere_lab_buildout.md) for the process
  
