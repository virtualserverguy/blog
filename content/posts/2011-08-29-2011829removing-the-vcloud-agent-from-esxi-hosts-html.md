---
title: "Removing the vCloud agent from ESXi hosts"
date: "2011-08-29"
tags: 
  - "vcloud"
  - "vsphere-5"
---

In order to remove the vCloud agents from vSphere 5 hosts you need to execute the following command on the console:

> esxcli software vib remove –n vcloud-agent

This can be ran by the PowerCLI or the vSphereCLI or on the SSH console with tech support mode enabled.

Reboot the hosts after this step to complete the removal.
