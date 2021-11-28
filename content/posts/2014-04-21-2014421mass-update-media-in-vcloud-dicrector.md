---
title: "Mass Update Media in vCloud Dicrector"
date: "2014-04-21"
categories: 
  - "vmware-vcloud"
tags: 
  - "powershell"
  - "vcloud"
---

In vCloud 5.1 it is very difficult to move media from LUN to LUN once it is uploaded. In vCloud 5.5 this gets better but it is still a pain.

One method I have found that works is to disable the LUN you want the media moved off of, and change something on the media record. Something such as adding a ' ' (space) to the description will cause vCloud Director to copy the media to a new LUN.

Below is a script to mass update media entries to allow them to move easier.

```PowerShell
$MediaToUpdate = Get-Catalog -Org NAME | Get-Media 
Foreach ( $Media in $MediaToUpdate ) { 
  $RefMedia = Get-Media -Id $Media.Id
  Write-Host “Updating “ $RefMedia.Name 
  $OldDescription = $RefMedia.Description 
  $OldDescription += "." 
  $Media.ExtensionData.Description = $OldDescription 
  $Media.ExtensionData.UpdateServerData 
}
```

Just make sure the LUN you want cleaned off is 'disabled' and you have enough space on the other LUNs for the newly copied/moved media.
