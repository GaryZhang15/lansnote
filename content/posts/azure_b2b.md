---
title: "Azure AD B2B federation authentication"
date: 2021-08-30T15:00:11+08:00
draft: false
---

# Overview

![B2B](/azure_b2b/azure_b2b_auth_overview.jpg "Azure B2B auth flow")

Supported IdPs
> Below IdP also support self-service sign-up user flow
- Azure AD
- Microsoft Account
- Facebook
- Google

# General Guide
## Sign-in endpoints
SAML/WS-Fed IdP federation guest users can also use application endpoints that include your tenant information, for example:

- https://myapps.microsoft.com/?tenantid=<your tenant ID>
- https://myapps.microsoft.com/<your verified domain>.onmicrosoft.com
- https://portal.azure.com/<your tenant ID>
- https://myapps.microsoft.com/signin/Twitter/<application ID?tenantId=<your tenant ID>

## Determine if partner needs update DNS text records
1. If partner IdP is well know IdPs, no DNS changes are needed.
    - okata.com
    - my.salesforce.com
    - accounts.google.com
    - etc.
2. If auth URL is same as target domain, no DNS changes are needed
3. If auth URL is different from target domain, then need add the following DNS  record to verify the auth URL
    - `fabrikam.com.  IN   TXT   DirectFedAuthUrl=https://fabrikamconglomerate.com/adfs`

## SAML 2.0 configuration (partner)
- ACS: `https://login.microsoftonline.com/login.srf`
- Audience: urn:federation:MicrosoftOnline (This value will be **deprecated**. https://login.microsoftonline.com/<tenant ID>/ Recommended tenanted audience.) 
- Claim:
    - NameID format: `urn:oasis:names:tc:SAML:2.0:nameid-format:persistent`
    - emailaddress: `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

## WS-Fed configuration (partner)
> Two WS-Fed providers have been tested for compatibility with Azure AD include AD FS and Shibboleth.
- PassiveRequestorEndpoint:	`https://login.microsoftonline.com/login.srf`
- Audience: urn:federation:MicrosoftOnline (This value will be **deprecated**. https://login.microsoftonline.com/<tenant ID>/ Recommended tenanted audience.) 
- Claim:
    - ImmutableID `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`
    - emailaddress `http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress`

## Azure AD configuration (Host)
This step is very simple. Follow the steps [here](https://docs.microsoft.com/en-us/azure/active-directory/external-identities/direct-federation#step-3-configure-samlws-fed-idp-federation-in-azure-ad).

One thing worth mention is that the domain name field is used to for home realm discovery for partner, which will be the target domain name for federation.

# References

[Federation with SAML/WS-Fed identity providers for guest users (preview)](https://docs.microsoft.com/en-us/azure/active-directory/external-identities/direct-federation)

[WS-Fed/SAML with ADFS](https://docs.microsoft.com/en-us/azure/active-directory/external-identities/direct-federation-adfs)

