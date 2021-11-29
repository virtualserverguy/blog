---
title: "Detecting and Removing Invalid vApps"
date: "2014-04-09"
categories: 
  - "vmware-vcloud"
tags: 
  - "powershell"
  - "vcloud"
---

After you run vCloud for a while, heck run any management product for a while, and you will have left overs, hung items, or even corrupt vApps.

With vCloud Director you can run the below to find those items and remove them.

```PowerShell
$badvapp = Search-Cloud -QueryType AdminVapp | Where-Object { $_.Status -eq "UNRESOLVED" }
foreach ( $id in $badvapp ) {
  Get-CIVApp -Id $id.id | Remove-CIVApp
}
```

This probably wont remove everything, those items that are left, generally can only be removed via editing the database though, I would not recommend that.