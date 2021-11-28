---
title: "Nesting Resource Pools; Good Idea or Bad?"
date: "2011-12-15"
categories: 
  - "vmware-vsphere"
tags: 
  - "resource-pools"
  - "vsphere"
---

I was asked recently on my opinion on nesting resource pools with VMs inter-mixed, well what should you do?

Well here is an easy example; if I have a Resource Pool with 9 VMs and 1 nested Resource Pool, what level of resources are each given?  10% each.

Think about that, each of the VMs have 10% of the resources and the ENTIRE nested Resource Pool has 10% of the resources.  

How many VMs are in that nest Resource Pool?  Lets assume 10 VMs.

What entitlement to the resources does a single VM in the nested Resource Pool have?  10% of the nested Resource Pools resources, which is 10% of the parents Resource Pool. So this one VM will get 1% of the parent Resource Pools resources.

How can this problem be fixed? A better practice is to not have Resource Pools and VMs to exist at the same level of the tree. The above example would be changed to have 2 Resource Pools under the parent Resource Pool. One Resource Pool could be named 'prod' and the other Resource Pool named 'development'. The 'prod' Resource Pool would be given normal shares and the 'development' Resource Pool would be given low shares.  

So now what is the resource allocation to each?

The 'prod' Resource Pool will have 2/3 of the total parent Resource Pool, and the 'development' Resource Pool would have 1/3 of the parent Resource Pool.  This still does not guarantee that 'prod' will have access to resources. This setting is just a guarantee that in a contention scenario, that 'prod' will be given higher priority to resources.

How can you guarantee resources to 'prod'?  Reservations for the 'prod' Resource Pool or setting a limit on the 'development' Resource Pool.
