---
title: "vCloud Director and VMware Horizon Intergration"
date: "2013-03-20"
---

# Requirements for SSO in vCloud Director

The SAML process and parties using them have formal roles and responsibilities:

- Service Provider – An entity that receives the SAML Message from an Idenity Provider (vCloud Director )
- Identity Provider – An entity that authenticates an user (Horizon)

The Identity provider must provide these fields in the response (case sensitive):

- UserName
- EmailAddress
- FullName
- Groups

While the only required field is UserName it is recommended that all fields be returned with proper information to allow for ease of management and administration of the users and their rights.

# Configuring vCloud Director

In vCloud director you will first need to enable the use of a SAML Identity provider.

1. Once logged in as a Organization Administrator or System Administrator go to the organization Administration page, click on Federation, then enable the ‘Use of SAML Identity Provider’ 
1. The XML metadata file that you got from your SAML/SSO provider should be downloaded to the machine these actions are running from. Due to the use of special characters and copy/paste issues it is not recommended to paste in a value into the field. Instead use the upload function to upload the XML file in whole.

> In the case of VMware's Horizon Product the metadata can be found here: https:///SAAS/API/1.0/GET/metadata/idp.xml

1. Now close the organization tab or log out and back into the UI to get the ‘Groups’ and Import from SAML options in the UI. After that is completed you can now import users into vCloud Director.

Since SAML users and groups are not searchable users will have to be added one per line for each role. Another option for granting access to the organization is through the use of groups.

At this point the configuration of vCloud Director is complete.

## Exporting XML Metadata from vCloud Director

We now need to export a file much like what we imported from the SAML provider, so that the SAML provider will trust and validate requests coming from vCloud Director. This file and related certificates are controlled on the Federation page where we imported the SAML XML file. At the bottom of the page click on the ‘Regenerate’ button to create a new certificate with a validity of 1 year.

It will prompt you with a warning about changing the certificate. If you have already setup a SAML provider relationship, changing this certificate will break that relationship until the SAML provider replaces their current information with the new certificate. Once the certificate is generated you can download it via this weblink: https://./cloud/org//saml/metadata/alias/vcd Save this file as an XML file, then provide this to your SAML provider for the next section.

# Configuring Horizon for vCloud Director SSO

First you will need to login to the administrator interface for Horizon and create a new Application, then follow these configuration items for that application.

1. Configure the Login Redirection URL to be the organization URL in vCloud Director. This is required for vCloud Director to work properly, since the authentication sequence must start with vCloud Director and not Horizon.
1. Check the ‘Include the Destination in the response’
1. Check the Sign the entire response.
1. Check the ‘Sign the assertion’
1. Remove the ‘Include Cert’ checkbox
1. Select the configure via Meta-data XML option. Then upload the certificate (copy/paste) the certificate in to the text box given.
1. Click on ‘Populate Attribute Mapping’
1. Configure the Attribute Mapping to match your deployment of Hoizon.
