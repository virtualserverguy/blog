---
title: "Detecting and Removing Invalid vApp Templates"
date: "2014-04-07"
categories: 
  - "vmware-vcloud"
tags: 
  - "powershell"
  - "vcloud"
---

In the event that a vApp Template or Catalog Item fails during the upload process parts of that vApp Template can be left behind. To find and remove those items run the following:

```PowerShell
$badvappt = Search-Cloud -QueryType AdminVappTemplate | Where-Object { $_.Status -eq "FAILED_Creation" }
foreach ( $id in $badvappt ) {
  Get-CIVAppTemplate -Id $id.id | Remove-CIVAppTemplate -RemoveCatalogItem $false
}
```

Run the first part to see what there is, run it all to remove broken vApp Templates.

You will need to download the custom powershell pack from [here](http://velemental.com/2012/05/05/unofficial-vmware-vcd-cmdlets/).
