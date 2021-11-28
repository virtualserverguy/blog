---
title: "vSphere Disk Write Process"
date: "2011-09-01"
categories: 
  - "microsoft-hyper-v"
tags: 
  - "disk"
  - "san"
  - "vsphere"
---

Recently I have seen quite a bit of question and discussion of how vSphere handles disk writes from the guest OS and performance questions about limiting the writes.

The question started off innocently as "How can we gaurantee vSphere disk writes happen and are not cached?"

First lets analyze where this may have started SQL Solutions posted this [article](http://sqlsolutions.com/articles/articles/SQL_Server_and_VMware-A_Potentially_Fatal_Combination.htm), in which they tested SQL server on a VMware virtual machine and tested the write caching of the DB and the virtual machine.  The fatal flaw with this test is that they used VMplayer which is NOT vSphere and works nothing like vSphere does with disk writes.  VMplayer (as well as Workstation and Fusion) does cache results (which is what they have shown), where as vSphere behaves completely differently.

vSphere writes are handled differently since vSphere is an Enterprise server class software product.  Each and every write that a guest does is not confirmed in the operating system until it has been confirmed by the underlying storage array.  vSphere since ESX 3.x has behaved like this.

This is true for NFS and SCSI based storage.

Does that mean that the data actually made it to a spindle?  NO

vSphere only knows that the storage array has confirmed the write has happened, it could still be in the cache of the storage array, this could be the cache of the RAID controller or the SAN storage array.  Now most of these enterprise storage class arrays have built in batteries to write all items in the cache to disk system in the event of a power failure; but that is out of the vSphere control.

So how do you maintain storage consistancy and data integrity?  The simple answer is use enterprise storage and ensure that the battery backed cache or UPS for the array can either outlast the power outage (i.e. generator power up or utilities being restored).

Options like FUA (Force Unit Access) are not feasible since modern HBA's, RAID controllers, SAN's and file systems strip this control bit from the IO, also to use FUA for this each and every I write IO would require the FUA bit to be set.
