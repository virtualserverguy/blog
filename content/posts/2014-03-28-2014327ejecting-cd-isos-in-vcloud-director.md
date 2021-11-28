---
title: "Ejecting CD ISO's in vCloud Director"
date: "2014-03-28"
categories: 
  - "vmware-vcloud"
tags: 
  - "powershell"
  - "vcloud"
---

With vCloud Director 5.1 every once in a while a CD will refuse to eject, or worse it will say it ejected the CD but it will not make the change in vCenter.

To get around this with PowerCLI connected to the vCenter use this command:

```PowerShell
get-folder | get-VM | Get-CDDrive | Set-CDDrive -NoMedia -Confirm:$false
```

This will allow the CD to be ejected without having to Deploy, Eject, Re-Capture the vApp Template. To use for a normal vApp use the vApp Name/UUID.
