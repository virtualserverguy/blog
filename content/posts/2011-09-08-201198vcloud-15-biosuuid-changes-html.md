---
title: "vCloud 1.5 Bios.UUID Changes"
date: "2011-09-08"
categories: 
  - "vmware-vcloud"
tags: 
  - "vcloud"
  - "vsphere"
---

With vCloud 1.x and even back in Lab Manager 3.x and 4.x the default behavior for capturing and deploying VMs to the Library (LM term) or Catalog (vCloud term) has been to keep the BIOS.UUID the same for all subsequent VMs.  This allows those products that tie their license to the machine serial number to keep workign when re-deployed on vCloud or LM.  

Let's back up what is the BIOS.UUID?  The BIOS.UUID is randomly generated when the VM is created on vSphere, this value can be duplidated on a vSphere or vCenter instance, meaning it is not a unique identifier.  The BIOS.UUID is what the VM or guest queries when it looks for the 'machine serial number'.  Hence when a software product (Microsoft Windows, SQL, and other vendors products) look for a way to identify what machine it is installed on it uses the machine serial or BIOS.UUID.  If we go changing this value we can break software licenses or installations since the value is no longer the same as when it was installed.

Problems arise from this when software products report back to a central database with the machine name and machine serial number for compliance checks or other needs.  For example if I have a domain controller and SQL server with the same BIOS.UUID (they may have been deployed from the same vCloud Catalog entry) with Trend Micro (or most other A/V products) installed.  When that product reports the status of the installed A/V back to the control center, there is a conflict: I have two macines with different names but the same serial number reporting back.  Most products will only report the last machine to report in for its status, so I could have a system that has a very old A/V definitions but never know it due to the conflict in serial numbers.

With vCloud 1.5 there is a database entry that can be changed to allow for vCloud on deployment from catalog entries that will change the BIOS.UUID of each VM; but this will cause problems with software products that will either require re-activation or re-entering the license key since that product may indicate that the underlying machine is different.

How to make the change:

- In the vCloud database (either SQL or Oracle), in the CONFIG table there is an entry named: backend.cloneBiosUuidOnVmCopy
- Change the default value of 1 to 0 to force vCloud to start changing BIOS.UUID's
- Restart the VMware vCloud Service on all vCloud Director cells

This will NOT change currently deployed VMs and is a cloud wide setting affecting ALL VMs/vApp's being deployed from now on (or until changed back to 1).
