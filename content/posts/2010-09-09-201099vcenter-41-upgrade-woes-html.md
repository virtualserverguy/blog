---
title: "vCenter 4.1 Upgrade Woes"
date: "2010-09-09"
categories: 
  - "vmware-vsphere"
---

Recently while upgrading a customers vCenter database to 4.1 from 4.0 I ran in to this gem of a problem.  The problem is created when you change the schema of the account that accesses the database.  So if you have a user that is in the dbo schema then you change that user to something like VPXAdmin for the schema the upgrade will break on you.  When using the regular installer we received a message that the schema's did not match.  
  
So normally you should login to SQL and verify that the schema's match or that it didn't change on you.  But if for some reason you sign in and don't see anything wrong here is some more steps to lead you down a rabbit hole.  
  
To complete a DB upgrade without using the full fledged installed you can run the VCDatabaseUpgrade utility from the installation media under the vpxdbupgradebin directory.  The command to use is like this  

> VCDatabaseUpgrade.exe DSN=<DSN Name> UID=<Username with DB rights> PWD=<Password>

  
This will attempt to run the wizard as that user; if for some reason nothing happens you should check out the logs in this location (the username is the user that is attempting to launch the utility which may not be the same user that has DB rights):  
  
Windows 2008 and newer:  

> C:Users<Username>AppDataLocalTemp2

  
Windows 2003:  

> C:Documents and Settings<Username>Application DataLocalTemp2

  
This log file will show something such as:  

> \[9/8/2010 4:10:39 PM\] Initialize failed, exiting...  
> \[9/8/2010 4:10:45 PM\] Info: Beginning upgrade process....  
> \[9/8/2010 4:10:45 PM\] Info: vCenterTest\_SQLNativev10 has been detected as a SQL server.  
> 
> \[9/8/2010 4:10:45 PM\] Error: ERROR \[28000\] \[Microsoft\]\[SQL Server Native Client 10.0\]\[SQL Server\]Login failed for user 'administrator'.  
> ERROR \[28000\] \[Microsoft\]\[SQL Server Native Client 10.0\]\[SQL Server\]Login failed for user 'administrator'.  
>   

  
If the wizard starts up click next and start.  If all goes well then it will upgrade your database without any issue or error (but then again you wouldn't be reading this if you didn't have an error).  The mismatched schema causes issues about 3/4 of the way through the first file with this line in the logs:  

> create table vpx\_device\_tmp (DEVICE\_ID NUMERIC(38) identity(0,1), DEVICE\_NAME nvarchar(255))  
> SET IDENTITY\_INSERT dbo.vpx\_device\_tmp ON

  
What quickly stuck out at me is that the script is creating a table vpx\_device\_tmp without specifying the schema to use, meaning that it uses the users default (which in my case had been changed).  So instead of getting a table with dbo.vpx\_device\_tmp we get something like VPXAdmin.vpx\_device\_tmp; which then breaks on the very next command when SQL tries to locate and set the Identity on the table.  
  
So how do we fix this little problem?  
  
First we need to roll back the database to pre-upgrade status (that is why you took a backup prior to starting this process!  Sure we could continue from here but there is about 700 lines of SQL code that need to be backed out otherwise you will get errors when attempting to re-run it such as this error:  

> ALTER TABLE VPX\_HOST ADD BOOT\_TIME\_ON\_HOST NUMERIC(21) null  
>   
> \[9/8/2010 4:18:16 PM\] Error: Failed to execute command: ALTER TABLE VPX\_HOST ADD BOOT\_TIME\_ON\_HOST NUMERIC(21) null  
>   
> \[9/8/2010 4:18:16 PM\] Got exception: ERROR \[42S21\] \[Microsoft\]\[SQL Server Native Client 10.0\]\[SQL Server\]Column names in each table must be unique. Column name 'BOOT\_TIME\_ON\_HOST' in table 'VPX\_HOST' is specified more than once.  
>   
> \[9/8/2010 4:18:16 PM\] Error while upgrading: ERROR \[42S21\] \[Microsoft\]\[SQL Server Native Client 10.0\]\[SQL Server\]Column names in each table must be unique. Column name 'BOOT\_TIME\_ON\_HOST' in table 'VPX\_HOST' is specified more than once.  
>   
> \[9/8/2010 4:18:16 PM\] Info: Exiting Upgrade Wizard  
>   
> \[9/8/2010 4:20:59 PM\] Info: Flushing all logs and quitting application.

  
So after we roll back, we need to modify the default schema from the incorrect value to the dbo value that it was installed with.  Once that is complete re-start the upgrade and watch as it completes without error (unless you are really unlucky).  
  
VMware probably should have caught this problem in QA but since it is a pretty bizarre test case I am sure they will add it next time, :).  Or they could just make sure to use fully qualified tables in their upgrade scripts and not even have to worry about something like this.
