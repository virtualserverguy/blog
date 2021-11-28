---
title: "vCenter Installation Tips"
date: "2010-07-13"
categories: 
  - "vmware-vsphere"
---

Since the vCenter now requires a 64 bit operating system to install, the DSN must be upgraded as well to support the 64bit application.  Currently vCenter 4.0 and older all required a 32 bit DSN.  To change to the proper DSN you will need to remove the old one from the 32-bit DSN application and create a new DSN.  
  
1) Remove the old DSN if it exists from: %windir%SysWoW64ODBCAD32.exe  
  
2) Install the 64 bit SQL native client from: [http://go.microsoft.com/fwlink/?LinkId=123718&clcid=0x409](http://go.microsoft.com/fwlink/?LinkId=123718&clcid=0x409 "SQL Native Client for 2008 R1 and R2")  
  
3) Create a new DSN from the utility in Administrative Tools or here: %windir%system32ODBCAD32.exe (this is the 64 bit version)  
  
4) Install vCenter and get rocking and rolling.
