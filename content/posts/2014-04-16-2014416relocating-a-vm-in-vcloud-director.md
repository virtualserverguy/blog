---
title: "Relocating a VM in vCloud Director"
date: "2014-04-16"
categories: 
  - "vmware-vcloud"
tags: 
  - "powershell"
  - "vcloud"
---

Occasionally I need to move a VM or vApp from datastore to datastore, various reasons why. Sometimes I need to break the linked clone tree and force vCenter to consolidate it. Sure I can power off the VM and execute a 'consolidate' via the UI, but what if I need to keep the VM powered on? A storage vMotion does just that.

Sure you can fire up your vCenter Client or WebClient and move the VM that way. If you like your cloud / VM and like them running I would not do that.

Instead run this tid-bit of code in a PowerShell window.

To move a vApp:

```PowerShell
$destDatastoreName = “LUN NAME"
$vm\_names = Get-CIVApp "VAPP NAME" | get-civm
foreach ($vm in $vm\_names) {
  $dsQuery = Search-Cloud -QueryType Datastore -Name $destDatastoreName
  $dsRef = New-Object vmware.vimautomation.cloud.views.reference
  $dsRef.Href = "https://$($global:DefaultCIServers\[0\].name)/api/admin/extension/datastore/$($dsquery.id.split(':')\[-1\])" $vm.ExtensionData.Relocate($dsRef)
}
```

To move a single VM:

```PowerShell
$destDatastoreName = “LUN NAME"
$vm\_name = get-civm "VM NAME"
$dsQuery = Search-Cloud -QueryType Datastore -Name $destDatastoreName
$dsRef = New-Object vmware.vimautomation.cloud.views.reference
$dsRef.Href = "https://$($global:DefaultCIServers\[0\].name)/api/admin/extension/datastore/$($dsquery.id.split(':')\[-1\])" $vm.ExtensionData.Relocate($dsRef)
```
An important rule to remember... a VM can only live on 1 datastore, this means all VMDK's and the VMX of that VM must exist on the same datasore. Executing the above will make sure that happens. If you fell like breaking things and use the vSphere Client, keep this in mind.
