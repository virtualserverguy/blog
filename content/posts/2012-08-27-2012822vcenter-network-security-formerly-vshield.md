---
title: "vCloud Network Security (formerly vShield)"
date: "2012-08-27"
---

Those of you that used the former product vShield that is OLD news, VMware's marketing team has renamed it to be VMware vCloud Network Security, which is really what it is. vShield EndPoint is now free with vSphere host licenses, Enterprise Plus is needed of course.

Here is a highlight of what is new in vCloud Network Security:

- The Edge product finally supports more than two interfaces, and becomes a more flexible and usable product. It now features 10 interfaces, it can be a mix of internal and external interfaces.
- Edge now has an SSL VPN built in to it, this is truly interesting with vCloud Deployments. Instead of needed an IPSec VPN client, and the underlying requirements (looking at you GRE), now the requirement is port 443.
- The new UI... can't say enough about it. It is clearly a ground up re-design from the old design. Now it is more standard, easier to follow, and much easier to add/change/delete rules.
- Throughput - Edge is now 'officially' supporting > 3Gb/s with 2,000 NAT and 2,000 Firewall rules. 'Unofficially' it tested much higher than that.
- Load Balancer is actually getting smarter now, it is not just the round-robin as it was before, it now will do load balancing policies.
