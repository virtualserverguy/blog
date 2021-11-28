---
title: "Error in vCenter when creating a PvDC in vCloud Director"
date: "2011-07-22"
tags: 
  - "vcenter"
  - "vcloud"
  - "vsphere"
---

If your vCloud Director machine is on the same vCenter as the Compute Clusters are (not a best practice but it does work), you can not have the same vCloud Director machine name in vCenter as you named the vCloud installation during installation.

This will produce an error such as “The <PvDC Name> already exists.”

This is because vCenter Folders and Virtual Machines can not have identical names.  Can the host name be the same?  Sure!  You just can not have a VM Display name and a PvDC Name the same.

How do you fix it?

Rename the offending VM’s name (i.e. add -cell1 to the end) or drop the vCloud DB and re-run the installation to re-create the vCloud Instances name.
