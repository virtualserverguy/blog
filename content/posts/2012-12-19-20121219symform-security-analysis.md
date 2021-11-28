---
title: "Symform Security Analysis"
date: "2012-12-19"
---

This morning on twitter I was asked if Symform "Secure Online Backup" was as secure as SpiderOak (my favorite online storage/backup solution). Here is my analysis from reading Symform's publically facing documents.

## How it works:

According to Symform's website, your data is processed at the folder level. Meaning that all files in a folder are encrypted together. This does give the benefit of being able to de-duplicate the files inside that folder, it is not clear if this is at the block or file level though. If done at the block level this would be analogous to compression, if done at the file level I would image not much savings in space since it is uncommon for duplicate files in the same folder.

These files are encrypted with AES256 (good job there), but what generates this key? Since there would be a separate key per folder/container it would be near impossible for the end user to manage these keys. That means the Symform Cloud Control is generating and managing these keys for you the end user. (This is confirmed by their own documentation)

After your files are encrypted (in 64MB folder chunks), they are then broken into 1MB chunks. Parity fragments are then generated out of those 1MB chunks, 32 parity fragments to be exact. Those parity chunks are then sent out to the Symform Global Cloud Storage Network, and distributed to 96 devices.

## Analysis:

That seems fine right? Your data is spread among 96 random devices on the internet, encrypted and secure.

Well that is the problem, who controls the decryption/encryption keys? Symform does. Who controls where your data is stored on this 'Global Cloud Storage Network? Symform does.

From a stand point of Trust No One, Symform fails the test. A hacker can still get your AES keys, and the location of those blobs on the internet. A government agency can still subpoena for your data, and have access to the decrypted data.

While it looks like a neat technology, SpiderOak still wins in my opinion, since I control the encryption keys and where my data resides (Amazon S3 storage).
