<!--
net_config/dns-build.md
-->

# DNS build
### VM Creation Walkthrough

Download the Ubuntu 16.04 ISO:
http://releases.ubuntu.com/releases/16.04/ubuntu-16.04.4-server-amd64.iso
(From: http://releases.ubuntu.com/releases/16.04/)

- In Fusion, Create a New VM by clicking the '+' sign
- Choose the .iso file, it should auto-detect as Ubuntu Linux
- Un-check "Use Easy Install"
- Configure VM before installing (choose 'configure' at the end of the vm creation wizard)
- Save the VM in a single place with the rest of your lab
- Configure the VM:
  - Assign 1 CPU and 512MB of RAM
  - Remove the Sound Card
  - Disable 3D Acceleration ("graphics")
  - Remove the Printer
  - Remove the Camera
  - Remove the USB Controller
  - Configure the Network Adapter to use vmnet2
    - Generate MAC Address, copy it to the vmnet2 dhcpd config
    - Make sure 'connected' is checked
  - Add a 2nd VM, assign it to the vmnet7 network
    - No MAC generation needed, we can let it happen automatically
    - Make sure "connected" is checked


Power up the VM and see that it gets the right IP addresses, then run an apt update / upgrade to grab bug and security patches.

Now we can get to configuring [bind9](http://www.bind9.net) using [this document](./net-dns_config).
