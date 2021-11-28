---
title: "SpiderOak v. Sugar Sync"
date: "2012-04-27"
categories: 
  - "technology"
tags: 
  - "cloud-storage"
---

I recently moved from Sugar Sync with over 60GB stored to SpiderOak for cloud based storage of documents, pictures and other data. Before I explain why here is a quick overview on how they work differently (based on the documentation on their web sites).

### SugarSync

Data is transmitted unencrypted to SugarSync through a encrypted  SSL/TLS connection to the SugarSync servers. The data is then encrypted and stored on the SugarSync servers for later retrieval. This means that if SugarSync is 'hacked' or subpoenaed by a law enforcement agency they can have access to all of your data.

While I do not store sensitive information outside of secure containers (think TruCrypt files), it still concerned me enough to find a new cloud storage provider.

### SpiderOak

SpiderOak does things differently, they do not want to know what information you store or how to get to it. Data is encrypted on the local machine before it is sent over a SSL/TLS connection to the SpiderOak servers. The key is based off the password that is used to create the account. This means that SpiderOak does not know your password or the encryption key for your data. Which ultimately means that if they are subpoenaed by a law enforcement agency, the only data that they can hand over is a jumble of random data bits.

Is there a perfect solution of course not; given enough time and enough resources any encryption method will fail. SpiderOak utilizes AES256 for their encryption. Assuming 10 billion billion keys per second, it would take 3 x 10^51 years; longer than the data I store is usable (barely).

If you want to try SpiderOak here go [here](http://www.spideroak.com). First 2GB is free, after that for $75/yr you can get 75GB (use the promo code 'spring'), normally it is $100. Unlimited computers and devices, 100GB stored (compressed/de-duplicated) data.
