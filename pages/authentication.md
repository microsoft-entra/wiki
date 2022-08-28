

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

### 1.3.1 Password Protection for Active Directory (on premise)

[Azure AD Password Protection](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad-on-premises) detects and blocks known weak passwords and their variants, and can also block additional weak terms that are specific to your organization. On-premises deployment of Azure AD Password Protection uses the same global and custom banned password lists that are stored in Azure AD, and does the same checks for on-premises password changes as Azure AD does for cloud-based changes. These checks are performed during password changes and password reset events against on-premises Active Directory Domain Services (AD DS) domain controllers.

## 2. Blocking legacy authentication

Legacy authentication is a term that refers to an authentication request made by:

- Older Office clients that do not use modern authentication (for example, Office 2010 client)
- Any client that uses legacy mail protocols such as IMAP/SMTP/POP3

Legacy authentication does not support multi-factor authentication (MFA). Even if you have an MFA policy enabled on your directory, a bad actor can authenticate using a legacy protocol and bypass MFA. The best way to protect your account from malicious authentication requests made by legacy protocols is to [block these attempts altogether](https://docs.microsoft.com/azure/active-directory/fundamentals/concept-fundamentals-block-legacy-authentication).


## 3. Temporary Access Pass (TAP)

A [Temporary Access Pass (TAP)](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-temporary-access-pass) is a time-limited passcode issued by an admin that satisfies strong authentication requirements and can be used to onboard other authentication methods, including Passwordless ones such as Microsoft Authenticator or even Windows Hello. A TAP also makes recovery easier when a user has lost or forgotten their strong authentication factor like a FIDO2 security key or Microsoft Authenticator app, but needs to sign in to register new strong authentication methods.

### 3.1 Admin experience

Before anyone can sign-in with a TAP, admin needs to [enable](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-temporary-access-pass#enable-the-temporary-access-pass-policy) TAP in the authentication method policy and choose which users and groups can sign in by using a TAP and lifetime of passes created in the tenant.

After admin enables a policy, they can [create a TAP](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-temporary-access-pass#create-a-temporary-access-pass) for a user in Azure AD. From the user profile page, select **Add authentication methods**, and choose **Temporary Access Pass**. 

The following screenshot shows how to create a TAP:

![](./media/authentication/temporary-access-pass-1.png)

Once added, the details of the TAP are shown. Make a note of the actual TAP value. You provide this value to the user. You can't view this value after you select Ok. The following screenshot shows a TAP create by administrator:

![](./media/authentication/temporary-access-pass-2.png)

### 3.2 User experience

The most common use for a TAP is for a user to register authentication details during the first sign-in or device setup, without the need to complete extra security prompts. Authentication methods are registered at <https://aka.ms/mysecurityinfo>. Users can also update existing authentication methods here.

Note, you can also test the TAP by navigating to the <https://myapps.microsoft.com> portal, or any other application.

User enters the UPN of the account you created the TAP for, such as emily@contoso.com.

![](./media/authentication/temporary-access-pass-3.png)

If the user is included in the TAP policy, they'll see a screen to enter their TAP. The user needs to enter the TAP that was displayed in the Azure portal.

![](./media/authentication/temporary-access-pass-4.png)
