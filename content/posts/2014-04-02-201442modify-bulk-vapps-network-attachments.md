---
title: "Modify Bulk vApp Network Attachments"
date: "2014-04-02"
categories: 
  - "vmware-vcloud"
tags: 
  - "powershell"
  - "vcloud"
---

With vCloud Director if you need to change the Organization vDC Network, for instance you run out of IP addresses. You can use the script below to change the attached network of all powered off vApps.

> $vapps = search-cloud -QueryType VAppOrgNetworkRelation | Where-Object { $_.OrgNetworkName -eq "Old Network Name" -and $_.Status -eq "Stopped” }
> 
> foreach ($vapp in $vapps) {
> 
> get-civapp -id $vapp.id | Get-CIVAppNetwork -ErrorAction SilentlyContinue | Where-Object { $\_.ConnectionType -eq "Routed" } | Set-CIVAppNetwork -ParentOrgNetwork "New Network Name"
> 
> Write-Host "Updated " $vapp.id " Owned by: " $Vapp.OwnerName
> 
> }

Simply change the New Network Name and Old Network Name in the commands above.
