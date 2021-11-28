---
title: "vCenter Configuration Manager Split Install Issues"
date: "2012-04-12"
categories: 
  - "vmware-vcm"
tags: 
  - "configuration-manger"
  - "vcenter"
  - "vcm"
---

vCM or vCenter Configuration Manager 5.5 was released in March by VMware with a few new features. First of all and the topic of this blog post, is the re-inclusion of a split install. Split install being the database, application and web page can be on different servers.You ask didn't vCM or SCM or ECM (depending on when you used vCM last) have this feature before? It did back in the 5.4 and earlier, in 5.4.1 VMware removed the feature so that it could be re-engineered and designed.The split install in vCM 5.5 allows for 3 different installs; all in one, database on one server and app/web on another, or all on separate servers. The SQL Reporting Server can be anywhere as long as it is reachable.Those familiar with vCM's install will know that something called 'Foundation Checker' will dig through your system and find any missing dependencies or bad settings.

### Now for the gotcha…

vCM expects that the database server name and the name in the connection string to be the same. In a single server (or all in one) install Foundation Checker will check this for you. In a split install Foundation Checker runs at the start of the install and not after you enter all the settings for vCM.While going through the install the you supply the DB server name, what is entered here MUST be what SQL returns for this command:

> use master; select @@servername

If you need to change what is returned to be a FQDN or something other than what is returned do this now, before continuing the install (you will thank me later). MS MSDN has a good write up on how to do this [here](http://msdn.microsoft.com/en-us/library/ms143799.aspx).

### What happens if I ignore the above?

Well first off the Install will complete without error; however the collector service will not stay started post install. SQL logs will have errors like 'ECMStatusUser' not defined or not allowed login. The collector service will start then stop about 5 - 10 seconds later without error in the Windows event log.

### How can you fix this after the install completes?

The easy answer is to un-install and re-install. If you are dead set on getting the thing to work here is what you can do.First you will need to run some SQL commands.

> sp\_helpserver

Take note of the name of the server returned. Now we need to drop that server.

> sp\_dropserver <name>

You will get errors about remote logins when doing this. This is due to vCM creating logins that really do not work or exist during the install due to SQL configuration issues. To force the removal use this command.

> sp\_dropserver <name>, droplogins

Now you will need to re-add the correct server name, add what you typed into the installer (i.e. the FQDN) with.

> sp\_addserver <name>, local

Restart the SQL service. Now you can start the vCM Collector service. This will get your installation working, there are some other things inside of vCM that will need correcting. For instance you need to do a machines collection from the collector, then you will need to re-trust the vCM collector.Again I recommend that you just uninstall and re-install with the correct settings. You will however need to fix SQL and make sure that the server name is correct.
