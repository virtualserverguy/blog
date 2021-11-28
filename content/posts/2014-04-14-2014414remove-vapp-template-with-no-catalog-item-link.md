---
title: "Remove vApp Template With No Catalog Item Link"
date: "2014-04-14"
categories: 
  - "vmware-vcloud"
tags: 
  - "powershell"
  - "vcloud"
---

First... Did you know that vApp Templates and Catalog Items are two different things in vCloud Director? If so, did you know that you can have a vApp Tempalte that does not link to a catalog item? Finally, you can't have a Catalog Item without a vApp Tempalte backing though.

Well I guess you could. If you manage to get one of those, you will want to follow my guide on fixing that [here](http://virtualserverguy.com/blog/2014/3/31/find-broken-catalog-items-in-vcloud-5x).

Okay back to detecting if you have a vApp Template that is not mapped to a Catalog Item. To detect these 'hung' vApp Templates run the following script as a 'system administrator'

```Powershell
$VappTemplates = Search-Cloud -QueryType AdminVappTemplate

foreach ( $VappT in $VappTemplates ) { $vAppTemplate = Get-CIVAppTemplate -ID $VappT.Id
  $vapptid = $vapptemplate.id
  $CatItem = Search-Cloud -QueryType AdminCatalogItem -Filter Entity==$VappTId
  if ( !$CatItem ) { Write-Host "Get-CIVappTemplate -ID $($vAppTemplate.Id) " }
}
```

This will procduce an out put of 'Get-CIVappTemplate' and the ID of the hung vApp Template. It is up to you to pick what to do with that hung vApp Template. I recommend removing them and re-creating whatever they were. To do that append this to the output and run it in the same PowerShell window:

```PowerShell
Remove-CIVappTemplate -RemoveCatalogItem $False
```