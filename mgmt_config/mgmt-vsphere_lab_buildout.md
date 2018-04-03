<!--
mgmt-vsphere_lab_buildout.md
-->

# vSphere Lab Buildout
Once the vCSA is up and you have one or more hosts on the network and responding to their dns hostnames, we can begin adding those hosts to vSphere and start building the lab.

## Create Virtual Data Center


A virtual data center is a container for all the inventory objects required to complete a fully functional environment for operating virtual machines. You can create multiple data centers to organize sets of environments. For example, you might create a data center for each organizational unit in your enterprise or create some data centers for high-performance environments and others for less demanding virtual machines.
Prerequisites

In the vSphere Web Client, verify that you have sufficient permissions to create a data center object.
Procedure

- In the vSphere Web Client, navigate to the vCenter Server object.
- Select Actions > New Datacenter.
- Rename the data center and click OK.


#### What to do next

Add:
- (Virtual) [hosts](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.vcenterhost.doc/GUID-CCE2AEC1-FE9F-4387-8EBF-512CB4B51B26.html)
- [clusters](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.vcenterhost.doc/GUID-B1018F28-3F14-4DFE-9B4B-F48BBDB72C10.html)
- [resource pools](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.resmgmt.doc/GUID-60077B40-66FF-4625-934A-641703ED7601.html),
- [vApps](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.vm_admin.doc/GUID-E6E9D2A9-D358-4996-9BC7-F8D9D9645290.html),
- [networking](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.networking.doc/GUID-35B40B0B-0C13-43B2-BC85-18C9C91BE2D4.html),
- [datastores](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.storage.doc/GUID-8AE88758-20C1-4873-99C7-181EF9ACFA70.html),
- [virtual machines](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.vm_admin.doc/GUID-55238059-912E-411F-A0E9-A7A536972A91.html)
