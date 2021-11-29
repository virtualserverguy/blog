---
title: "Find Broken Catalog Items in vCloud 5.x"
date: "2014-03-31"
categories: 
  - "vmware-vcloud"
tags: 
  - "powershell"
  - "vcloud"
---

Sometimes when uploading content into vCloud there is a chance that the content can be broken. This can cause programs to have errors. To find these items, run the following in PowerShell as the a 'system administrator'.

```PowerShell
search-cloud -QueryType AdminCatalogItem | Where-Object { $_.Status -eq "Unknown" }
```

You can now remove them utilizing the API or vCO and the 'Remove Catalog Item' workflow.
