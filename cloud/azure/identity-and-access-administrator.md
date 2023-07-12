---
description: >-
  Cheatsheet for the SC-300 Microsoft Identity and Access Administrator
  certificate
---

# Identity and Access Administrator

## Key points

* Tenant name: xxx.onmicrosoft.com, can use custom domain&#x20;
* Entitlement Management / Identity Governance: P2, access package (role, policy) -> catalog
* Access Review: P2, who (self, manager, delegated, multistage), recurrence, action
* Privileged Identify Management: P2, roles / resources assignment of active (perm) / eligible (temp elevation) with all kinds of granular settings (duration, MFA, etc)
* Email OTP for non AD user and non Microsoft user valid for 30 mins by default

## Azure AD Connect

* Connects and sync between on prem AD and cloud Azure AD
* Uses connector spaces to import / export on prem / Azure AD into metaverse
* Cloud Sync: instead of syncing on prem, sync in cloud with lightweight agents on prem for communication
* Shown as Directory Synced in Azure AD, attribute changes mostly from on prem AD only
* Hard match: on prem AD `ms-DS-ConsistencyGuid` (Base64) = Azure AD `sourceAnchor`
* Soft match: try matching proxy address, user principal name, etc
* Password hash sync: hash of pw hash, used for authentication / check dark web leakage

## External accounts

* Default as guest, can be turned into member
* `New-AzureADMSInvitation`
* Bulk invite: email + redirection URL
* Use linked subscription for monthly active users

## Authentication

1. Cloud authentication: direct auth at Azure AD, can use pw hash sync as fail over
2. Pass through authentication: added to auth queue at Azure AD, agents check queue and auth at on prem AD, then pass result back to Azure AD
3. Federation: Azure AD redirect auth to federation service (eg ADFS), which checks with on prem AD and return SAML token to user to be used at Azure AD

* SSPR: self service password reset, could be email, phone, mobile app code, security questions
* Combined security information registration experience: MFA + SSPR
* Smart lockout: remembers last 3 wrong passwords and won't get counted for threshold&#x20;

<table><thead><tr><th width="305.3333333333333">Method</th><th width="209">Primary authentication</th><th>Secondary authentication</th></tr></thead><tbody><tr><td>Windows Hello for Business</td><td>Yes</td><td>MFA</td></tr><tr><td>Microsoft Authenticator app</td><td>Yes</td><td>MFA &#x26; SSPR</td></tr><tr><td>FIDO2 security key</td><td>Yes</td><td>MFA</td></tr><tr><td>OATH hardware tokens</td><td>No</td><td>MFA &#x26; SSPR</td></tr><tr><td>OATH software tokens</td><td>No</td><td>MFA &#x26; SSPR</td></tr><tr><td>SMS</td><td>Yes</td><td>MFA &#x26; SSPR</td></tr><tr><td>Voice call</td><td>No</td><td>MFA &#x26; SSPR</td></tr><tr><td>Password</td><td>Yes</td><td></td></tr></tbody></table>

## Groups

* Security: permissions vs M365: collaboration
* Assigned: specified user vs Dynamic user / device: based on query of attributes
* If assign roles to group, membership type can only be assigned, can not be dynamic

## Roles

* Custom role: only permissions for Application registrations and Enterprise applications
* Application administrator: add, manage, configure enterprise apps (eg registration, SSO, license) and on prem (eg app proxy)
* Cloud application administrator: cloud apps only without on prem (app proxy)

## Administrative units

* Limit permission scope to unit
* Can add users and groups
* Permissions are applied users only, not applied to group members

## Device registration

1. Azure AD Register: personal device, local auth with SSO, use MDM to check compliance
2. Azure AD Join: corporate owned, auth at Azure AD
3. Hybrid Join: corporate owned, joins on prem AD and registers at Azure AD through Azure AD Connect

## Conditional Access

* P1+ feature, use security defaults instead for lower license levels
* Assignment
  * Users / workload identities: can include and exclude users, groups, externals, roles
  * Cloud apps / user actions: all / selected apps, register security information / device action
  * Conditions: user / sign in risks, device platforms, locations, client apps, device filter
* Access control
  * Grant: MFA, approved app, hybrid joined, pw change, compliant device, terms of use, etc
  * Session: app enforced restriction, app control (defender for cloud apps), sign in frequency, persistent browser session, continuous access evaluation, disable resilience defaults
* Risk
  * Supported by P2 feature: Identity Protection
  * Sign in risk: only anonymous IP address & unfamiliar sign in properties are considered as conditional access sign in risk, other offline ones are just for reporting

## Emergency access account

* Not user specific
* Cloud account
* Will not expire
* Global admin
* Does not use phone MFA
* Excluded from conditional access
* Rotate password every 90 days

## Application integration

1. Assign users and groups
2. Set up SSO: SAML, OpenID Connect, OAUTH 2.0
3. Provision user accounts
4. Conditional access
5. Self service
