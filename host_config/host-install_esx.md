<!--
host_config/host-install_esx.md
-->

## Host: Install ESXi Virtual Host

Installing ESXi 6.5 in VMware Fusion is a painless process.

### Overview

- Download ESXi .ISO file from [MyVMware](https://my.vmware.com/group/vmware/details?downloadGroup=ESXI65U1&productId=614&rPId=21946)
- Open VMware Fusion 10 and choose 'File > New' or click the '+' button from the Virtual Machine Library.
- Select the .ISO file for ESXi
  - (current version is *"VMware-VMvisor-Installer-6.5.0.update01-5969303.x86_64")*
- Click 'Customize Settings' at the end of the walkthrough
- Save the file
- Remove the Camera
- Remove the USB/Bluetooth controller
- Adjust CPU/Memory according to hardware capabilities.
  - My iMac Pro lab has 3 virtual ESXi hosts, 4CPU + 16GB of RAM each.
  - Minimum host size is 2CPU +4GB of RAM (also is what is assigned by default)
  - In general you need to leave at least 1 for the Host Mac.
  - On a 4-physical core machine you have 8 "logical" cores you can assign (because of HyperThreading).  So you could deploy the VCSA and 1 minimum-sized Host before starting to hit resource limits.
- Configure Network Adapters
  - Assign first NIC to 'Bridged, Autodetect'
  - Add new NIC
  - Assign new NIC to 'Share with my Mac' (should do this by default)
    - This will be the network that nested VMs live on

Once the VM boots it should walk you through the installation parameters.
- Use the 'Fn' button to access Function keys like F11 to begin the installation.
- Use the standard keyboard layout
- Choose the installation disk
- Set the Root password
- The system makes a few checks, you can then push F11 to begin the installation.
  - I find it always looks like it's frozen around 27%, so just let it sit and finish. It shouldn't be more than 5-7 minutes depending on the speed of your Mac.


**You now can quickly log into the Host and configure it's networking.**

Follow [this document](./host-setup_vhosts.md) for information about configuring the Virtual ESXi Host after it's been installed: [host-setup_vhosts.md](./host-setup_vhosts.md)

Repeat for each Virtual ESXi Host required.

Full Cloning is not advised as the storage device UID's would not change, causing a conflict in vCSA when trying to add Host 2 and more.
Each ESXi host must be installed.
