---
title: "Monitoring Compute Performance of a VM"
date: "2014-03-31"
categories: 
  - "vmware-vcloud"
  - "vmware-vsphere"
tags: 
  - "monitoring"
  - "performance"
  - "vcloud"
---

Even when using vC Ops from VMware, vCenter metrics, vCloud Metrics, and Hyperic Montoring there are things that can be missed.

What if the datastore shows 1ms latency on the vSphere host, the CPU usage is low, the Memory is not being swapped, but a user insists it is just 'slow'. What would you check?

In our cloud deployment (25,000 VMs in a single vCloud instance, and we have 4); I have deployed 4 - 6 VMs per vCenter across differnet datastores, on different hosts. These VMs are 512MB of RAM, 16GB of Hard Drive, and 1 vCPU. On these VMs I installed CentOS, MySQL and sysbench.

sysbench for those that do not know runs artificial tests against the HDD, RAM, CPU and MySQL. Since we have the CPU, RAM and HDD monitored by other products, I configured it to only point at the MySQL server. The MySQL test will test every portion of the compute stack. While the RAM and CPU may report within acceptable ranges, they maybe high in those ranges. Combinded that may cause a performance impact.

My script runs every 5 minutes via a cron job, and logs the data to a SQL database, for later reporting and analysis.

I won't cover how to install sysbench or MySQL here, since that can be found else where on the internet. [sysbench](http://www.serveradminblog.com/2010/02/sysbench-on-centos-howto/) & [MySQL](http://dev.antoinesolutions.com/mysql)

You will also need to install iSQL for CentOS, to write your data to a SQL server (if that is your target), those instructions can be found [here](http://wiki.sysconfig.org.uk/display/howto/OBDC+on+CentOS+5.2).

After you have the above installed and ready, you can run the following to get a report on the status of your VMs performance:

> sysbench --num-threads=16 --max-requests=10000 --test=oltp --oltp-table-size=500000 --mysql-socket=/var/lib/mysql/mysql.sock --oltp-test-mode=complex --mysql-user=root --mysql-password=VMware1! run > mysql.sysbench
> 
> $testvaule = cat mysql.sysbench | egrep " cat|transactions:" | awk {'print substr($3,2) '}
> 
> $date = date -u "+%F %R"
> 
> $machine = ifconfig eth0 | grep inet | awk '{ print substr($2,6) }’
> 
> $hostname = hostname
> 
> inssql="insert into TABLENAME VALUES (‘$date', ‘$machine', ‘$testvalue’,’$hostname')"
> 
> echo $inssql | isql HOSTNAME USERNAME PASSWORD

The above will insert the data in to a SQL table, for later reporting.

Keep in mind you do not want to make a 'monster' VM, the smaller the better, you want to tax all of the components. If you give it 4GB of RAM, then MySQL will cache all of the disk I/O in RAM and not report an accurate number. If you give it 4 vCPU's you may actually artificially lower your score by causing the hypervisor to schedule 4 vCPUs worth of tasks. In this case smaller is most definitely better.

This will not replace the other monitoring solutions you may have, but it will help to augment those solutions.
