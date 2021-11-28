---
title: "Enabling SAML Providers in vCloud 5.1"
date: "2013-02-23"
categories: 
  - "vmware-vcloud"
tags: 
  - "security"
  - "vcloud"
---

As a system or organization administrator head to the 'Administration' page, and then the federation tab. Paste or upload the SAML configuration XML. Ensure the certificate at the bottom of the page is recent, if not click re-generate certificate. It will produce a certificate for 1 year.

After the certificate is re-newed enter this URL in to the web browser: `cloud/org/\[orgName\]/saml/metadata/alias/vcd ;` save the XML file on that page. This is the file you will need to provide the SAML or 3rd party authentication service with in order to authenticate you.

Now you have SSO or SAML or 3rd authentication, enabled on your organization. Once configured/enabled the Org login page will now use the SAML provider, meaning any local users will be locked out.
