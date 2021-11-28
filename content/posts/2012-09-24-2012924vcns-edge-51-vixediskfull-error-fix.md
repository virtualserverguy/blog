---
title: "vCNS Edge 5.1 VIX_E_DISK_FULL ERROR Fix"
date: "2012-09-24"
---

VMware this morning released a KB article and a fix for the Edge devices filling up on disk space. While it did not kill the edge or cause an outage, it did stop you from being able to make changes to the Edge's configuration.

The official fix will be released on this site: https://my.vmware.com/web/vmware/info/slug/security_products/vmware_vcloud_networking_and_security/5_1

The upgrade/patch will require the standard vCloud Network Security (vShield) upgrade process where the Edge device will need to be replaced with the new code. (READ: Possible outage of network for a few moments while the Edge is swapped)

How do you know if you have this problem?

In vCloud Director, attempting a reconfig fails with this error:

> VIX_E_DISK\_FULL

In vCloud Director, when looking at Edge Gateways, you receive this error:

> Edge VM backing the edge gateway is unreachable

Just remember, when this happens it is not causing an outage or a network failure. The edge is basically running 'headless' at that time, and will not accept any ruleset changes.
