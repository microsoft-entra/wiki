

# Authentication

## 1. Password protection

### 1.1 Password policies (complexity and more)

- A [password policy](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad-combined-policy#azure-ad-password-policies) is applied to all user and admin accounts that are created and managed directly in Azure AD. 
- The Azure AD password policy doesn't apply to user accounts synchronized from an on-premises AD environment using Azure AD Connect unless you enable the EnforceCloudPasswordPolicyForPasswordSyncedUsers flag.
- You can't change these settings except as [noted in this table](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad-combined-policy#azure-ad-password-policies).

### 1.2 Password expiration policies

#### 1.2.1 Tenant level settings

The following are the [password expiration policies](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad-combined-policy#password-expiration-policies) you configure on the tenant lever that impact all users in the directory:

- Password expiry duration. Default value: 90 days.
- Password expiry notification (When users are notified of password expiration). Default value: 14 days before password expires.

#### 1.2.2 User level settings

The following are the [password expiration policies](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad-combined-policy#password-expiration-policies) you configure per user:

- A global administrator or user administrator can use the [Microsoft Azure AD Module for Windows PowerShell](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0) to set user passwords not to expire.
- By default, only passwords for user accounts that aren't synchronized through Azure AD Connect can be configured to not expire. For more information, [Connect AD with Azure AD.](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-password-hash-synchronization#password-expiration-policy). This impact all users that are sync via the Azure AD Connect.

## 1.3 Banned password list

The Azure AD Identity Protection team constantly analyzes Azure AD security telemetry data looking for commonly used weak or compromised passwords. Weak terms are added to the [global banned password list](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad). When a password is changed or reset for any user in an Azure AD tenant, the current version of the global banned password list is used to validate the strength of the password.

- The global banned password list is automatically applied to all users in an Azure AD tenant. There's nothing to enable or configure, and can't be disabled. 
- This global banned password list is applied to users when they change or reset their own password through Azure AD.
- Admin can add their own entries to the [custom banned password list](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad#custom-banned-password-list)

## 2. Blocking legacy authentication

Legacy authentication is a term that refers to an authentication request made by:

- Older Office clients that do not use modern authentication (for example, Office 2010 client)
- Any client that uses legacy mail protocols such as IMAP/SMTP/POP3

Legacy authentication does not support multi-factor authentication (MFA). Even if you have an MFA policy enabled on your directory, a bad actor can authenticate using a legacy protocol and bypass MFA. The best way to protect your account from malicious authentication requests made by legacy protocols is to [block these attempts altogether](https://docs.microsoft.com/azure/active-directory/fundamentals/concept-fundamentals-block-legacy-authentication).

