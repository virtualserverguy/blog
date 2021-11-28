---
title: "How to change the UUID of a VM via the PowerCLI"
date: "2011-02-18"
categories: 
  - "vmware-vsphere"
---

In vCloud director it may be necessary to deploy an identical vApp, when this happens everything is identical (including UUID's), to help vSM differentiate the VMs changing the UUID may help.

  

$date = get-date -format "dd hh mm ss"

  

$newUuid = "56 4d 50 2e 9e df e5 e4-a7 f4 21 3b " + $date

  

$spec = New-Object VMware.Vim.VirtualMachineConfigSpec

  

$spec.uuid = $newUuid

  

$vm = get-vm <VM Name>

  

echo "VM: " $VM.name "New UUID: " $newuuid

  

$vm.Extensiondata.ReconfigVM\_Task($spec)

  

  

Original credit goes to this man and site: [http://derek858.blogspot.com/2010/10/making-your-vmware-vm-uuids-unique.html](http://derek858.blogspot.com/2010/10/making-your-vmware-vm-uuids-unique.html)
