

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

### 1.3 Banned password list

The Azure AD Identity Protection team constantly analyzes Azure AD security telemetry data looking for commonly used weak or compromised passwords. Weak terms are added to the [global banned password list](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad). When a password is changed or reset for any user in an Azure AD tenant, the current version of the global banned password list is used to validate the strength of the password.

- The global banned password list is automatically applied to all users in an Azure AD tenant. There's nothing to enable or configure, and can't be disabled. 
- This global banned password list is applied to users when they change or reset their own password through Azure AD.
- Admin can add their own entries to the [custom banned password list](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad#custom-banned-password-list)

#### 1.3.1 Password Protection for Active Directory (on premise)

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

## 4. Certificate-based authentication

[Certificate Based Authentication (CBA)](https://docs.microsoft.com/azure/active-directory/authentication/concept-certificate-based-authentication) enables administrators to allow or require users to authenticate with X.509 certificates against their Azure AD for applications and browser sign-in.

Before this feature brought cloud-managed support for CBA to Azure AD, customers had to use AD FS to be able to authenticate using X.509 certificates against Azure AD. There are some [limitations](https://docs.microsoft.com/azure/active-directory/authentication/concept-certificate-based-authentication-limitations) you should be aware of. 

The CBA is type of passwordless authentication. On-premises passwords need not be stored in the cloud in any form.

### 4.1 Admin experience

There are some configuration steps to complete before enabling Azure AD CBA. For more information, check out the [How to configure Azure AD certificate-based authentication](https://docs.microsoft.com/azure/active-directory/authentication/how-to-certificate-based-authentication) article.

To configure the certification authorities you can use [Azure Portal](https://docs.microsoft.com/azure/active-directory/authentication/how-to-certificate-based-authentication#configure-certification-authorities-using-the-azure-portal), or [PowerShell](https://docs.microsoft.com/azure/active-directory/authentication/how-to-certificate-based-authentication#configure-certification-authorities-using-powershell)

### 4.2 User experience

During sign-in, users enter their username into the Azure AD sign-in page, and then select **Next**. Then the users will see an option to authenticate with a certificate instead of entering a password. If multiple matching certificates are present on the device, the user can pick which one to use. The certificate is validated, the binding to the user account is checked, and if successful, they are signed in.

The following screen shows the first sign-in page where the user enters their UPN:

![](./media/authentication/certificate-based-authentication-1.png)

The following screen shows the second sign-in page where a user can select to **Sign in with a certificate**:

![](./media/authentication/certificate-based-authentication-2.png)

Note, if admin has enabled other authentication methods like Phone sign-in or FIDO2, users may see a different sign-in screen.

#### 4.2.1 Windows SmartCard logon

Azure AD users can authenticate using X.509 certificates on their [SmartCards directly against Azure AD at Windows logon](https://docs.microsoft.com/azure/active-directory/authentication/concept-certificate-based-authentication-smartcard). There is no special configuration needed on the Windows client to accept the SmartCard authentication. A join machine or a hybrid environment (hybrid join) is required.

The user presents a physical or virtual SmartCard to the test machine. Then, select **SmartCard** icon, enter the PIN and authenticate the user.

![](./media/authentication/certificate-based-authentication-windows.png)

#### 4.2.2 Mobile devices

[Android and iOS devices](https://docs.microsoft.com/azure/active-directory/authentication/concept-certificate-based-authentication-mobile) can use certificate-based authentication (CBA) to authenticate to Azure AD using a client certificate on their device when connecting to:

- Office mobile applications such as Microsoft Outlook and Microsoft Word
- Exchange ActiveSync (EAS) clients

Azure AD certificate-based authentication (CBA) is supported for certificates on-device on native browsers as well as on Microsoft first-party applications on both iOS and Android devices.

## 5. Sign-in with email

You can configure Azure AD to let users [sign in with their email](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-use-email-signin) as an alternate login ID. For example, if Contoso rebranded to Fabrikam, rather than continuing to sign in with the legacy _ana@contoso.com_ UPN, email as an alternate login ID can be used. To access an application or service, users would sign in to Azure AD using their non-UPN email, such as _ana@fabrikam.com_.

The feature supports managed authentication with Password Hash Sync (PHS) or Pass-Through Authentication (PTA). The  'proxyAddresses' attribute is read-only and cannot be set using PowerShell.

The feature enables sign-in with ProxyAddresses, in addition to UPN, for cloud-authenticated Azure AD users. 

![](./media/authentication/email-signin.png)

This feature also supports [B2B guest user sign-in](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-use-email-signin#b2b-guest-user-sign-in-with-an-email-address) (cross tenant access) with an email address.