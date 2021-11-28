---
title: "vCNS App - Spoofguard Deployment"
date: "2012-09-25"
tags: 
  - "vcloud"
  - "vcloud-network-security"
  - "vshield"
---

Spoofguard records the IP address of each vNIC secured by vShield App. Spoofguard can be configured in two different modes, automatic and manual.

In Automatic mode the first IP that is presented for each vNIC is recorded and allowed to communicate without authorization. If the IP of the vNIC changes, the machine will no longer be able to communicate on the network until the new IP is approved.

In manual mode all IPs must be approved prior to being allowed to communicate; even existing virtual machines will be blocked until approved.

When enabling Spoofguard in an environment where there are existing virtual machines, it is recommended to enable Spoofguard in ‘Automatic’ mode. Once the vNICs are learned and reviewed it is then acceptable to switch to Spoofguard to ‘Manual’ mode, which will restrict all new virtual machines from communicating until approved. When deploying vShield App to a greenfield environment Spoofguard can be enabled with ‘Manual’ mode. Once Spoofguard has flagged a VNIC for approval, it must be approved prior to traffic being allowed to transmit. This is true even if Spoofguard is later disabled; all VNICs that are in ‘Require Approval’ will require approval before they can transmit.

When utilizing vShield App in a vCloud Director environment Spoofguard should not be enabled. The reason for this is that when vCloud Director brings a virtual machine online for the first time the machine will boot up and broadcast an IP (either DHCP or a pre-defined IP). When the machine is fully booted the guest customization script takes effect and changes the IP to the one defined in vCloud Director. Spoofguard will learn the first IP and not allow the VM to communicate on the network until the new IP is approved. It is possible to use vCenter Orchastrator to automate this approval process; that discussion and how to is out of the scope of this document.

Spoofguard currently supports only one IP per VNIC, so one cannot specify a secondary or failover IP.
