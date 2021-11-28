---
title: "vMotion Changes in vSphere 4.1"
date: "2010-08-19"
categories: 
  - "vmware-vsphere"
---

From VMware:  

> In vSphere 4.1:  
> VMDirectPath and USB Device Passthrough with vMotion is supported  
> Migration with vMotion and DRS for virtual machines configured with USB device passthrough from an ESX/ESXi host is supported  
> Fault Tolerant (FT) protected virtual machines can now vMotion via DRS. However, Storage vMotion is unsupported at this time.  
>   
> Note: Ensure that the ESX hosts are at the same version and build.  
> In addition to the above, vSphere 4.1 has improved vMotion performance and allows:  
> 4 concurrent VMotion operations per host on a 1GB network  
> 8 concurrent VMotion operations per host on a 10GB network  
> 8 concurrent VMotion operations per datastore

  
Finally VMware is allowing us to take advantage of the larger 10GBit pipes and allowing more than 1 vMotion at a time.
