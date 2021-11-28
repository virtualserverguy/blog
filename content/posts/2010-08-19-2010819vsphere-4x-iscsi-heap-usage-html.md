---
title: "vSphere 4.x iSCSI Heap Usage"
date: "2010-08-19"
categories: 
  - "vmware-vsphere"
---

When using more than 64 devices with the software iSCSI initiator the vmkernel logs will start to produce errors such as:  

> Jul 19 08:01:01 esx vmkernel: 0:03:38:54.053 cpu2:1039)**iSCSI:** bus 0 target 46 **cannot allocate new session** (size %Zu) at 10464  
> Jul 19 08:01:01 esx vmkernel: 0:03:38:54.054 cpu4:1040)**WARNING**: **Heap:** 1419: **Heap vmk-iscsi** (**6288144/6291456**): **Maximum allowed growth** (3320) **too small for size** (20480)

  
I most recently saw this problem crop up with a customer and a large XIV deployment to 32 vSphere hosts.  To resolve this problem we can increase the heap size to 8MB (from the default of 6MB) via this command:  

> esxcfg-module -s heap\_max=8388608 iscsi\_mod

  
Why 8388608?  Well this is the byte count (8 \* 1024 \* 1024 = 8388608).  Once this modification is complete a complete reboot of the ESX host is required to set this change.
