---
title: "vCenter Server Appliance Database"
date: "2012-02-24"
categories: 
  - "vmware-vsphere"
tags: 
  - "vcenter"
  - "vcenter-appliance"
  - "vsphere-5"
---

The vCenter Server Appliance comes with a built-in DB2 database for use as an all-in-one solution for small lab environments. The sizing is supposed to be less than 5 hosts and 50 VMs. But it can work much higher than that if given enough resources, :-).

One issue that occurs when using this appliance is that the DB2 log settings are too small for any extended operation. This is due to stat roll-up jobs taking more log space to complete than the DB2 instanace is set for. Symptoms of this will be your vCenter service resetting itself every so often, you can verify this happening by watching the vpxd.log file for the line "Transaction log full" and the service dying shortly after that. The way I found it is that my vSphere Client would disconnect and ask for me to log back in everyonce in a while.

The easy(-ish) fix for this is to do the following:  

  
2. SSH to the vCenter Appliance, if you left the default the username is 'root' and the password is 'vmware'. Once you are SSH'ed to the box you will need to change to the DB2 user.
  

>   
> su -l db2inst1  

  
6. Check your current log setting by running:
  

>   
> db2 get db cfg for vCDB | grep log  

  
This will show you something like this:  

>   
> User exit for logging status = NO
> 
> Catalog cache size (4KB) (CATALOGCACHE\_SZ) = 300
> 
> Number of primary log files (LOGPRIMARY) = 128
> 
> Number of secondary log files (LOGSECOND) = 16
> 
> Changed path to log files (NEWLOGPATH) =
> 
> Path to log files = /storage/db/db2/home/db2inst1/db2inst1/NODE0000/SQL00001/SQLOGDIR/
> 
> Overflow log path (OVERFLOWLOGPATH) =
> 
> Mirror log path (MIRRORLOGPATH) =
> 
> First active log file =
> 
> Block log on disk full (BLK\_LOG\_DSK\_FUL) = NO
> 
> Block non logged operations (BLOCKNONLOGGED) = NO
> 
> Percent max primary log space by transaction (MAX\_LOG) = 0
> 
> Num. of active log files for 1 active UOW(NUM\_LOG\_SPAN) = 0
> 
> Percent log file reclaimed before soft chckpt (SOFTMAX) = 520
> 
> User exit for logging enabled (USEREXIT) = OFF
> 
> HADR log write synchronization mode (HADR\_SYNCMODE) = NEARSYNC
> 
> First log archive method (LOGARCHMETH1) = OFF
> 
> Options for logarchmeth1 (LOGARCHOPT1) =
> 
> Second log archive method (LOGARCHMETH2) = OFF
> 
> Options for logarchmeth2 (LOGARCHOPT2) =
> 
> Failover log archive path (FAILARCHPATH) =
> 
> Number of log archive retries on error (NUMARCHRETRY) = 5  

  
13. To change the log file sizing run the following:
  

>   
> db2 UPDATE DB CFG FOR VCDB USING logprimary 128 logsecond 16 logfilsiz 8192  

  
17. For the setting to take effect you will need to reboot the appliance. Once the vCenter Appliance is running again you can check/watch the log files being created.
  

>   
> ls -lah /storage/db/db2/home/db2inst1/db2inst1/NODE0000/SQL00001/SQLOGDIR/
