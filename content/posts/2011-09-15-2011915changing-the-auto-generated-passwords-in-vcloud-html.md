---
title: "Changing the auto generated passwords in vCloud"
date: "2011-09-15"
categories: 
  - "vmware-vcloud"
tags: 
  - "guest-customization"
  - "vcloud"
---

In VMware's vCloud Director, when a VM is deployed using the guest customization, you can either supply a password for the administrator user or have vCloud auto-generate a password.  The auto-generated passwords are 8 characters long and use upper-case, lower-case, numbers and special characters for example "q#Tv21\*a".  If the 8 characters is not long enough for you you can increase the character length by changing a field in the database.

In both the Oracle and SQL database there is a field in the CONFIG table called 'AdminPasswordLength', simply change this field to be any number that you would like your passwords to be generated with.

Something like this:

> update config  
>   set value = 16  -- required length  
>   where cat = 'settings' and name = 'AdminPasswordLength';  
> commit;

Just do not go over 64 characters as you may get some un-expected results in the OS you are customizing.
