---
title: "netstat for ESXi"
date: "2012-01-31"
categories: 
  - "vmware-vsphere"
tags: 
  - "cli"
  - "esxi"
  - "vsphere"
---

With the removal of the service console with vSphere 5, in the form of ESXi, netstat went by the way side.  The way to get that information is by executing this on the console.  Either in tech support mode (SSH) or at the console.

> esxcli network ip connection list
