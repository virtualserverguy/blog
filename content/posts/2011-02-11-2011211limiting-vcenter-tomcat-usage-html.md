---
title: "Limiting vCenter TomCat Usage"
date: "2011-02-11"
categories: 
  - "vmware-vsphere"
---

Here is how to limit the memory usage for VMware's vCenter...  
  
First vCenter relies on a customized Apache Tomcat to run its vCenter product (mostly graphs, Web Interface and other items), while limiting the memory hasn't proven to have a negative effect this procedure should be done with caution. This can cause slowness in portions of the application since it will no longer be able to store large amounts of data in RAM and will have to access the database for this information.  

  
2. Open Regedit on the vCenter server
  
4. Navigate to: HKLMSoftwareWow6432NodeApache Software FoundationProcrun 2.0vctomcatParamatersJava
  
6. Change JvmMS, JvmMX and JvmSs to '0'
  

  
Restart the VMware vCenter WebAccess Service in Windows and enjoy a smaller footprint of the Tomcat process.  The average RAM usage for Tomcat after this change should be around 256MB (plus or minus the amount of VM's being managed).  
  
This procedure should only be done in test or small environments, anything over 10 hosts should follow the defaults from VMware (1024 and 512).
