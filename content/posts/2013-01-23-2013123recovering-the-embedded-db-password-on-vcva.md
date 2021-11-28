---
title: "Recovering the Embedded DB Password on VCVA"
date: "2013-01-23"
categories: 
  - "vmware-vsphere"
tags: 
  - "vcenter"
---

Here is how to recover the embedded DB password on the VMware vCenter Virtual Appliance (VCVA):

From the console (or SSH) of the VCVA run this command:

> grep EMB_DB_PASSWORD /etc/vmware-vpx/embedded\_db.cfg

From: http://kb.vmware.com/selfservice/microsites/search.do?language=en\_US&cmd=displayKC&externalId=2004506
