---
title: "Host Isolation Response Settings"
date: "2012-10-14"
categories: 
  - "vmware-vsphere"
tags: 
  - "vsphere"
---

Over the past few weeks I have had some people ask what I would recommend for host isolation addresses and responses, when using vSphere x.x with high availability (HA) enabled.

First off as with most everything in computers 'It depends'.

Items to consider with host isolation response is what type of storage is being utilized? Is it considered an outage if the vSphere hosts can talk to each other but the virtual machines (VMs) cannot? How stable is my management network? Is datastore heart-beating setup correctly? The list can of things to consider can be quite long.

Here is what I generally recommend…

## NAS Based Storage Options (iSCSI or NFS)

First, set one of the host isolation response addresses to the virtual IP (VIP) or the IP of the storage array. This will tell you if you can at least talk to the array; chances are that is you cannot talk to the array your machines have already failed.

That brings me to the isolation response, since the VMs should already be dead, remember the NAS array and host are no longer able to communicate, I recommend 'Power Off'. If you were to leave the response to 'Leave Powered On' you can run into a chance of corruption on the guest disks. Think about it, the disk goes away for 60 seconds, then comes back. Do you think that VM is going to be able to recover, what are the odds of it corrupting that vital disk? What about 'Shutdown Guest', well that has a chance of the same exact thing happening.

Power Off in this setting is the safest setting, not only will it allow for that VM to be brought up elsewhere, you run a less chance of corruption or VM failure.

## Fiber based storage (SAN)

With fiber the network isolation address does not matter as much, reason being the storage is not relying on the network for communication.

## General Host Isolation Techniques

If it is considered a down time for the VM network to fail but not the management network, is there a way we can mitigate this?

Of course, put a vmkernel port on the virtual machine network, enable it for HA traffic, then place an isolation address of that networks gateway in to the HA configuration.
