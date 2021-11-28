---
title: "vSphere 5 vRam Licensing Changes"
date: "2011-08-03"
categories: 
  - "vmware-vsphere"
tags: 
  - "vmware"
  - "vsphere"
---

When VMware released the vRam pricing models and limits last week there was quite an uproar over the limitations being set to low.  It appears that VMware was listening and has responded with a hefty increase in vRam allocations.

<table cellspacing="0" cellpadding="0"><tbody><tr><td class="td1" valign="top"><table class="t1" cellspacing="0" cellpadding="0" width="637.0"><tbody><tr><td class="td2" valign="bottom"><p class="p2"><strong>vSphere edition</strong></p></td><td class="td3" valign="bottom"><p class="p2"><strong>Previous vRAM entitlement</strong></p></td><td class="td3" valign="bottom"><p class="p2"><strong>New vRAM entitlement</strong></p></td></tr><tr><td class="td4" valign="top"><p class="p2"><strong>vSphere Enterprise+</strong></p></td><td class="td5" valign="top"><p class="p2">48 GB</p></td><td class="td5" valign="top"><p class="p2">96 GB</p></td></tr><tr><td class="td6" valign="top"><p class="p2"><strong>vSphere Enterprise</strong></p></td><td class="td7" valign="top"><p class="p2">32 GB</p></td><td class="td7" valign="top"><p class="p2">64 GB</p></td></tr><tr><td class="td4" valign="top"><p class="p2"><strong>vSphere Standard</strong></p></td><td class="td5" valign="top"><p class="p2">24 GB</p></td><td class="td5" valign="top"><p class="p2">32 GB</p></td></tr><tr><td class="td6" valign="top"><p class="p2"><strong>vSphere Essentials+</strong></p></td><td class="td7" valign="top"><p class="p2">24 GB</p></td><td class="td7" valign="top"><p class="p2">32 GB</p></td></tr><tr><td class="td4" valign="top"><p class="p2"><strong>vSphere Essentials</strong></p></td><td class="td5" valign="top"><p class="p2">24 GB</p></td><td class="td5" valign="top"><p class="p2">32 GB</p></td></tr><tr><td class="td6" valign="top"><p class="p2"><strong>Free vSphere Hypervisor</strong></p></td><td class="td7" valign="top"><p class="p2">8 GB</p></td><td class="td7" valign="top"><p class="p2">32 GB*</p></td></tr></tbody></table></td></tr></tbody></table>

That is nearly double the entitlements.

Also changing is how the usage is calculated for a high water mark (think bursting for a day) to a rolling 12 month average!

Finally the last news and some major news at that, is that a single VM can only consume 96GB of vRam, no matter how you set the VM up!  (i.e. give a VM 1TB of RAM but only have 96GB count against the vRam pool!)
