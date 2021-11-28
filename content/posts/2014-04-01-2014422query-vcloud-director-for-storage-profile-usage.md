---
title: "Query vCloud Director for Storage Profile Usage"
date: "2014-04-01"
categories: 
  - "vmware-vcloud"
tags: 
  - "powershell"
  - "vcloud"
---

Often times an organization will have multiple Storage Profiles, different class fo storage, etc. The simple command of:

> Get-OrgVDC

Returns a summary or cummulative view of the storage profile usage. To get the actual usage for each profile, execute this command:

> $OrgVdc = get-orgvdc (Org VDC Name)
> 
> search-cloud -querytype AdminOrgVdcStorageProfile | where { $\_.VdcName -eq $orgvdc } | get-ciview
