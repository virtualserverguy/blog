---
title: "Modify vSphere Path Selection Policy in Bulk"
date: "2010-09-22"
categories: 
  - "vmware-vsphere"
---

Recently, we upgraded a customer from ESX 4.0 update 2 to ESX 4.1 – except they didn’t want to upgrade, they insisted on clean installs.  Kickstart makes the deployment of new hosts easy, but they had around 40 of their hosts connected to 15 LUNs on an IBM XiV array.  Best practice for the XiV suggests a “round robin” path selection policy, but it defaults to MRU (Most Recently Used) on install – so they all needed to be changed.  
  
That’s a lot of clicking in the vSphere client…  
  
Enter vSphere PowerCLI!  
  
First, connect to your vCenter Server:  

**Connect-VIServer <vCenterServerName>**

  
Now, list all of the hosts and disks that are on the XiV array that are not set for RoundRobin:  

**Get-VMHost |\`  
Get-ScsiLun -LunType "disk" |\`  
where {$\_.MultipathPolicy –ne "RoundRobin" -and $\_.model -like "\*xiv\*"}|\`  
format-table VMHost,CanonicalName,MultiPathPolicy –autosize**

  
  
  
This one-liner (broken up for clarity):  

  
- connects to each host under management by the vCenter server
  
- gets SCSI LUNs of type “disk” (as opposed to a controller or something else) that have a MultiPath Policy that is _not_ Round Robin and also have a model name that includes “XIV” in the name.
  
- dumps a table listing the ESX host, the name of the LUN, and the current policy to the screen
  

  
OK, so now let’s change them all – instead of dumping a table to the screen, let’s pipe the results to the command **Set-ScsiLun -MultipathPolicy "RoundRobin"** .  The complete command is:  
  
**Get-VMHost |\`  
Get-ScsiLun -LunType "disk" |\`  
where {$\_.MultipathPolicy –ne "RoundRobin" -and $\_.model -like "\*xiv\*"}|\`  
Set-ScsiLun -MultipathPolicy "RoundRobin"**  
  
Of course, like all things PowerShell, the –whatif parameter is supported, so if you want to verify that it will do what you expect before actually making the change, append it to the end of command above.  
  
That’s it; all of the XiV LUNs are now set to Round Robin.  Verify this by running the first command again – there should be no output.
