---
title: "How to test vmKernel connectivity"
date: "2010-08-19"
categories: 
  - "vmware-vsphere"
---

In case you are ever stuck trying to get our iSCSI Initiator to link up to the target or just troubleshooting some vMotion problems you can do the following:  
  
From the console or terminal on a ESX host (CLI will work for ESXi as well) do teh following:  

> vmkping <destination>

  
This will use the vmk port groups to test connectivity to the iSCSI or other vSphere servers.  A good ping will result in a result like this:  

> PING server(10.0.0.1): 56 data bytes  
> 64 bytes from 10.0.0.1: icmp\_seq=0 ttl=64 time=10.245 ms  
> 64 bytes from 10.0.0.1: icmp\_seq=1 ttl=64 time=0.935 ms  
> 64 bytes from 10.0.0.1: icmp\_seq=2 ttl=64 time=0.926 ms

  
A failure of the ping is like this:  

> \[root@server\]# vmkping server  
> PING server (10.0.0.2) 56(84) bytes of data.  
>   
> \--- server ping statistics --- 
> 3 packets transmitted, 0 received, 100% packet loss, time 3017ms

  
This method will help to resolve the unable to connect to destination errors that a vMotion can produce
