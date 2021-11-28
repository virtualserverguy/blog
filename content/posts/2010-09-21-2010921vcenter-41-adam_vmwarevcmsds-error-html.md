---
title: "vCenter 4.1 ADAM_VMwareVCMSDS Error"
date: "2010-09-21"
categories: 
  - "vmware-vsphere"
---

Recently after upgrading to vCenter for a few customers the following started to appear in their Windows Event logs:

  

Active Directory Web Services encountered an error while reading the settings for the specified Active Directory Lightweight Directory Services instance.  Active Directory Web Services will retry this operation periodically.  In the meantime, this instance will be ignored.  Instance name: ADAM\_VMwareVCMSDS

  

To correct this you need to add the following to the registry:

  

>   
> 
> Key: HKLMSystemCurrentControlSetServicesVMwareVCMSDSParameters
> 
>   
> 
> Value: Port SSL
> 
>   
> 
> Type: REG\_DWORD
> 
>   
> 
> Data: 636

  

Restart the ADAM instance and the errors should stop.  (Unless of course you need something other than the default ports)
