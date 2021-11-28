---
title: "Importing vApp from vCenter Error"
date: "2011-08-24"
categories: 
  - "vmware-vsphere"
tags: 
  - "cisco-nexus"
  - "vcloud"
---

When importing a VM or vApp from vCenter into vCloud you may see an error like this:

>     A specified parameter was not correct.
> 
>     spec.deviceChange.device.port.switchUuid

This can happen when comign from a Cisco Nexus 1000v Portgroup, to solve this either remove the network adapter for importing into the cloud, or move the network card to a portgroup that is not a Nexus 1000v Portgroup.

If you are using a dVS and see this error move the NIC to a standard vSwitch or delete the NIC and re-add it once it is in the cloud.
