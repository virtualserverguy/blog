---
title: "VMware's New License Structure"
date: "2010-09-03"
categories: 
  - "vmware-vsphere"
---

As they announced in early August, they are now licensing SRM (as of Sept 1st, 2010) as a per protected VM model.  Meaning that you no longer have to license the entire cluster of VM's for SRM, you can select individual VM's to be protected by SRM.  So with that and the introduction of DRS Affinity inside of vSphere 4.1. 

DRS Affinity allows you to select which hosts the VM is allowed to be on inside the cluster (think DRS rules but super-fied)

  
Now just think of where else this can be applied...  
  
vSphere ESX Licenses on a per VM model?  

Makes since right?  Back when VMware started you could expect a 5 - 10 to 1 consolidation ratio, and now with Moore's law doubling transistors every year we can easily get 250 - 400 to 1 consolidation ratio.  So we are buying less vSphere per VM, which is not a sustainable model; so what option is left?  A per-VM model license, so if VM 'A' uses DRS, HA and vMotion it costs $50/yr (just a guess), but if VM 'B' uses HA and no vMotion it could cost just $25/yr (again, wild guess).

  

Think about what this can do for the market place and for those IT shops that struggle with charge back.  We can now assign pricing to the levels of SLA's that we give the end users!  Oh wait... VMware has a module to do that for us today [http://www.vmware.com/products/vcenter-chargeback/](http://www.vmware.com/products/vcenter-chargeback/)[http://www.vmware.com/products/vcenter-chargeback/](http://www.vmware.com/products/vcenter-chargeback/)

  
Of course I really have no idea that this may be happening, in fact I am sitting in a brewery so I may be completely off my rocker, but just think about it for a while, :) .
