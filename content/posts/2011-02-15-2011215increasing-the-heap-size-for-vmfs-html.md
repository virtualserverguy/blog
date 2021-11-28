---
title: "Increasing the heap size for VMFS"
date: "2011-02-15"
categories: 
  - "microsoft-hyper-v"
---

ESX 3.0 thru ESX 4.0 limit the heap size for VMFS to 16MB which allows for just 4TB of VMFS files to be open at a time.  Once this threshold is crossed the ESX host start to behave eradically, possible crashing the VMs that were powered on at the time.  To avoid this problem you can increase the heap size to 128MB which will allow for 32TB of storage open on a single ESX host.  
  
The vmKernel.log will display the following if your host is getting close to the limitation:  

> WARNING: Heap: 1370: Heap\_Align(vmfs3, 4096/4096 bytes, 4 align) failed. caller: 0x8fdbd0  
> WARNING: Heap: 1266: Heap vmfs3: Maximum allowed growth (24) too small for size (8192)

  
To correct this problem:  

  
2. Login to vCenter or use the VI client to connect directly to the ESX host in question
  
4. Click on the Configuration tab
  
6. Click Advanced Settings
  
8. Find and select VMFS3
  
10. Update the VMFS2.MaxHeapSizeMB to 128
  
12. Reboot the ESX host
  

  
ESX 4.1's default is 80MB which will allow for 20TB to be open at once, so it is less likely to run into this issue.  
  
Update: There is a VMware KB on this problem here: [http://kb.vmware.com/selfservice/microsites/search.do?language=en\_US&cmd=displayKC&externalId=1004424](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1004424)
