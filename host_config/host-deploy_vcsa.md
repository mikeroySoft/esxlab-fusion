<!--
host_config/host-deploy_vcsa.md
-->

# Deploying the vCenter Server Appliance

Deploying the vCSA on Fusion 10 is a simple task. You do not need to have any hosts waiting, and you can deploy right from Fusion Pro.

The process is as follows:
- Download the vCSA .iso file from VMware.com:
  - [Download link](https://my.vmware.com/group/vmware/details?downloadGroup=VC65U1G&productId=614&rPId=21946)
- Mount the .iso and copy/drag the .OVA file somewhere on your Mac
  - .iso is located in the 'vCSA' folder
- In Fusion choose File > Import and select the .OVA file
- Agree to the License and select a Server Size (Tiny vCenter Server with embedded PSC is sufficient for this lab)
- **Important!** Make sure you have the following filled out or the vCSA will fail to start and you will have to re-deploy.
  - **Networking Configuration**
    - Host IP Family
      - ipv4
    - Host Network Mode
      - 'static' or 'dhcp'
      - **NOTE:** There must be forward ***and*** reverse lookup for the IP that the vCSA gets in order for it to boot successfully.
    - Host Network IP Address
      - x.x.x.x or leave blank for DHCP
    - Host Network Prefix
      - use '24' for a /24 network
    - Host Network Default Gateway  
      - Enter if static, blank if DHCP
    - Host Network DNS Servers
      - Enter if static, blank if DHCP
      - This is the DNS server that ***must*** resolve forward and backward the IP address of this vCSA
    - Host Network Identity
      - FQDN of this host: **vcsa.esxlab.local**     
  - **SSO Configuration**
    - Directory Password
      - Because the Platform Services Controller is embedded, we are actually ***creating*** the password for the domain account.
  - **System Configuration**
    - Root Password
      - Create root password for vCSA Appliance management interface (https://vsa.esxlab.local:5480)
  - **Miscellaneous**
    - CEIP Enabled
      - VMware's anonymous telemetry program
  - **Domain Properties**
    - Domain Name
      - esxlab.local
    - Domain Search
      - esxlab.local (or blank)

From here verify your settings, click continue and save the appliance somewhere on your Mac.

From here the deployment kicks off, and should take a few minutes.

Once the Console in Fusion has the IP address on it you can visit https://vcsa.esxlab.local:5480 in your browser and access the Appliance Management Console.

From here you can begin installing your ESXi vHosts using [this document](./host-install_esx.md)



Full documentation of the vCenter Server Appliance can be found [here](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.vcsa.doc/GUID-3191913D-621E-4AA1-8F98-55CBB09E0C9F.html)  

For documentation about what to do *after* deployment, visit [this document](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.install.doc/GUID-5C6223B4-3E9E-4DD1-82D2-DCC78DFD5C18.html)

For documentation regarding vCenter Server and Host Management, visit [this document](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.vcenterhost.doc/GUID-3B5AF2B1-C534-4426-B97A-D14019A8010F.html)

Documentation regarding Organizing your vSphere Inventory (a great doc actually, especially for folks new to vSphere) can be found [here](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.vcenterhost.doc/GUID-4AE0FD7D-AA28-4A79-A634-A0432073E30C.html)
