---
title: "vSphere 4.1 ESX(i) Major Security Flaw"
date: "2010-07-21"
categories: 
  - "vmware-vsphere"
---

About a week ago while testing vSphere 4.1 upgrades and deployment methods, I signed into a host's service console as root, and I could have swore that I typed the password incorrectly.  So I signed back out and tried it again, and it let me in with an extra digit at the end of the password.  Some more testing led me to see that the PAM software was only checking the first 8 characters of the password and ignoring the rest of it.  
  
After some fancy Google'ing and wishing I found this article on the virtuallyGhetto blog:  [http://www.virtuallyghetto.com/2010/07/esxi-41-major-security-issue.html](http://www.virtuallyghetto.com/2010/07/esxi-41-major-security-issue.html)  
  
The good news is that VMware is aware of the issue and has a work around to correct the problem: [http://kb.vmware.com/selfservice/microsites/search.do?language=en\_US&cmd=displayKC&externalId=1024500](http://kb.vmware.com/selfservice/microsites/search.do?language=en_US&cmd=displayKC&externalId=1024500)  

#### VMware's Solution

**For ESX**:  
Add md5 to the file /etc/pam.d/system-auth.  

1. Log in to the service console and acquire root privileges. 
1. Change to the directory /etc/pam.d/. 
1. Use a text editor to open the file system-auth.
1. Add md5 to the following line, as shown:

```Shell
password sufficient /lib/security/$ISA/pam_unix.so use_authtok nullok shadow md5
```

Optionally, you can use the following sed command to accomplish this:

```Shell
sed -e /password.*pam_unix.so/s/$/ md5/ -i /etc/pam.d/system-auth
```
  

**For ESXi**:

Add md5 to the file /etc/pam.d/system-auth.

1. Access tech support mode.
1. Change to the directory /etc/pam.d/.
1. Use a text editor to open the file system-auth.
1. Add md5 to the following line, as shown:
  
```shell
password sufficient /lib/security/$ISA/pam\_unix.so use\_authtok nullok shadow md5  
```

(Optional) If you want the change to persist when you restart ESXi, you must add the following line to the file /etc/rc.local:

```Shell
sed -e '/password.*pam_unix.so.* md5/q' -e '/password.*pam_unix.so/s/$/ md5/' -i /etc/pam.d/system-auth
```

VMware expects to release a permanent solution to this issue sometime in the future. We recommend that you remove the workaround from ESXi systems when you install the permanent solution.