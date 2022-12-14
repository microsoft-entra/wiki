

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

## 3. Authentication, MFA methods and SSPR

Some [authentication methods](https://docs.microsoft.com/azure/active-directory/authentication/concept-authentication-methods) can be used as the primary factor when you sign in to an application or device, such as using a FIDO2 security key or a password. Other authentication methods are only available as a secondary factor when you use Azure AD Multi-Factor Authentication or SSPR.

The following table outlines when an authentication method can be used during a sign-in event:

| Method                         | Primary authentication | Secondary authentication  |
|--------------------------------|:----------------------:|:-------------------------:|
| Windows Hello for Business     | Yes                    | MFA\*                      |
| Microsoft Authenticator app    | Yes                    | MFA and SSPR              |
| FIDO2 security key             | Yes                    | MFA                       |
| OATH hardware tokens           | No                     | MFA and SSPR              |
| OATH software tokens           | No                     | MFA and SSPR              |
| SMS                            | Yes                    | MFA and SSPR              |
| Voice call                     | No                     | MFA and SSPR              |
| Password                       | Yes                    |                           |
| Security questions             | No                     | SSPR                      |

### 3.1 Password authentication

In Azure AD, a password is often one of the primary authentication methods. You can't disable the password authentication method. If you use a password as the primary authentication factor, increase the security of sign-in events using Azure AD Multi-Factor Authentication.

#### 3.1.1 Sign-in with email

You can configure Azure AD to let users [sign in with their email](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-use-email-signin) as an alternate login ID. For example, if Contoso rebranded to Fabrikam, rather than continuing to sign in with the legacy _ana@contoso.com_ UPN, email as an alternate login ID can be used. To access an application or service, users would sign in to Azure AD using their non-UPN email, such as _ana@fabrikam.com_.

The feature supports managed authentication with Password Hash Sync (PHS) or Pass-Through Authentication (PTA). The  'proxyAddresses' attribute is read-only and cannot be set using PowerShell.

The feature enables sign-in with ProxyAddresses, in addition to UPN, for cloud-authenticated Azure AD users. 

![](./media/authentication/email-signin.png)

This feature also supports [B2B guest user sign-in](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-use-email-signin#b2b-guest-user-sign-in-with-an-email-address) (cross tenant access) with an email address.

### 3.2 Certificate-based authentication

[Certificate Based Authentication (CBA)](https://docs.microsoft.com/azure/active-directory/authentication/concept-certificate-based-authentication) enables administrators to allow or require users to authenticate with X.509 certificates against their Azure AD for applications and browser sign-in.

Before this feature brought cloud-managed support for CBA to Azure AD, customers had to use AD FS to be able to authenticate using X.509 certificates against Azure AD. There are some [limitations](https://docs.microsoft.com/azure/active-directory/authentication/concept-certificate-based-authentication-limitations) you should be aware of. 

The CBA is type of passwordless authentication. On-premises passwords need not be stored in the cloud in any form.

#### 3.2.1 Admin experience

There are some configuration steps to complete before enabling Azure AD CBA. For more information, check out the [How to configure Azure AD certificate-based authentication](https://docs.microsoft.com/azure/active-directory/authentication/how-to-certificate-based-authentication) article.

To configure the certification authorities you can use [Azure Portal](https://docs.microsoft.com/azure/active-directory/authentication/how-to-certificate-based-authentication#configure-certification-authorities-using-the-azure-portal), or [PowerShell](https://docs.microsoft.com/azure/active-directory/authentication/how-to-certificate-based-authentication#configure-certification-authorities-using-powershell)

#### 3.2.2 User experience

During sign-in, users enter their username into the Azure AD sign-in page, and then select **Next**. Then the users will see an option to authenticate with a certificate instead of entering a password. If multiple matching certificates are present on the device, the user can pick which one to use. The certificate is validated, the binding to the user account is checked, and if successful, they are signed in.

The following screen shows the first sign-in page where the user enters their UPN:

<img src="./media/authentication/certificate-based-authentication-1.png" width="400">


The following screen shows the second sign-in page where a user can select to **Sign in with a certificate**:

<img src="./media/authentication/certificate-based-authentication-2.png" width="400">

Note, if admin has enabled other authentication methods like Phone sign-in or FIDO2, users may see a different sign-in screen.

##### 3.2.1.1 Windows SmartCard logon

Azure AD users can authenticate using X.509 certificates on their [SmartCards directly against Azure AD at Windows logon](https://docs.microsoft.com/azure/active-directory/authentication/concept-certificate-based-authentication-smartcard). There is no special configuration needed on the Windows client to accept the SmartCard authentication. A join machine or a hybrid environment (hybrid join) is required.

The user presents a physical or virtual SmartCard to the test machine. Then, select **SmartCard** icon, enter the PIN and authenticate the user.

<img src="./media/authentication/certificate-based-authentication-windows.png" width="400">

##### 3.2.1.2 Mobile devices

[Android and iOS devices](https://docs.microsoft.com/azure/active-directory/authentication/concept-certificate-based-authentication-mobile) can use certificate-based authentication (CBA) to authenticate to Azure AD using a client certificate on their device when connecting to:

- Office mobile applications such as Microsoft Outlook and Microsoft Word
- Exchange ActiveSync (EAS) clients

Azure AD certificate-based authentication (CBA) is supported for certificates on-device on native browsers as well as on Microsoft first-party applications on both iOS and Android devices.

### 3.3 Temporary Access Pass authentication

A [Temporary Access Pass (TAP)](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-temporary-access-pass) is a time-limited passcode issued by an admin that satisfies strong authentication requirements and can be used to:

- Onboard other authentication methods, including Passwordless ones such as Microsoft Authenticator or even Windows Hello.
- Recovery when a user has lost or forgotten their strong authentication factor like a FIDO2 security key or Microsoft Authenticator app, but needs to sign in to register new strong authentication methods.
- Alternative MFA method when an MFA device is not available. For example, a user forgot to bring their phone to the office, and need access to organization resource. 

In all of the scenarios above, an admin can issue a time-limited passcode allowing the user to security sign-in with the passwoce as a first or second factor authentication. 

#### 3.3.1 Admin experience

Before anyone can sign-in with a TAP, admin needs to [enable](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-temporary-access-pass#enable-the-temporary-access-pass-policy) TAP in the authentication method policy and choose which users and groups can sign in by using a TAP and lifetime of passes created in the tenant.

After admin enables a policy, they can [create a TAP](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-temporary-access-pass#create-a-temporary-access-pass) for a user in Azure AD. From the user profile page, select **Add authentication methods**, and choose **Temporary Access Pass**. 

The following screenshot shows how to create a TAP:

<img src="./media/authentication/temporary-access-pass-1.png" width="600">

Once added, the details of the TAP are shown. Make a note of the actual TAP value. You provide this value to the user. You can't view this value after you select Ok. The following screenshot shows a TAP create by administrator:

<img src="./media/authentication/temporary-access-pass-2.png" width="600">

#### 3.3.2 User experience

The most common use for a TAP is for a user to register authentication details during the first sign-in or device setup, without the need to complete extra security prompts. Authentication methods are registered at <https://aka.ms/mysecurityinfo>. Users can also update existing authentication methods here.

Note, you can also test the TAP by navigating to the <https://myapps.microsoft.com> portal, or any other application.

User enters the UPN of the account you created the TAP for, such as emily@contoso.com.

<img src="./media/authentication/temporary-access-pass-3.png" width="400">

If the user is included in the TAP policy, they'll see a screen to enter their TAP. The user needs to enter the TAP that was displayed in the Azure portal.

<img src="./media/authentication/temporary-access-pass-4.png" width="400">

### 3.4 Time-based One Time Password

[OATH TOTP](https://docs.microsoft.com/azure/active-directory/authentication/concept-authentication-oath-tokens#oath-hardware-tokens-preview) (Time-based One Time Password) is an open standard that specifies how one-time password (OTP) codes are generated. OATH TOTP authentication can be used as second factor authentication, not as a primary authentication.


OATH TOTP can be implemented using either software or hardware to generate the codes. Azure AD doesn't support OATH HOTP, a different code generation standard.


- [OATH software tokens](https://docs.microsoft.com/azure/active-directory/authentication/concept-authentication-oath-tokens#oath-software-tokens) - Software OATH tokens are typically applications such as the Microsoft Authenticator app and other authenticator apps. Azure AD generates the secret key, or seed, that's input into the app and used to generate each OTP.
- [OATH hardware tokens](https://docs.microsoft.com/azure/active-directory/authentication/concept-authentication-oath-tokens#oath-software-tokens) - Azure AD supports the use of OATH-TOTP SHA-1 tokens that refresh codes every 30 or 60 seconds. Customers can purchase these tokens from the vendor of their choice.
  - **Onboarding process**: Once tokens are acquired they must be uploaded in a comma-separated values (CSV) file format including the UPN, serial number, secret key, time interval, manufacturer, and model


### 3.5 Security questions

Security questions aren't used as an authentication method during a sign-in event. Instead, [security questions](https://docs.microsoft.com/azure/active-directory/authentication/concept-authentication-security-questions) can be used during the self-service password reset (SSPR) process to confirm who you are. Administrator accounts can't use security questions as verification method with SSPR.

When users register for SSPR, they're prompted to choose the authentication methods to use. If they choose to use security questions, they pick from a set of questions to prompt for and then provide their own answers.

#### 3.5.1 Admin experience

The admin configure the Security questions in Azure Portal => **Azure Active Directory** => **Password reset** => **Authentication methods**. It's not under the **Security** option like the other methods.

#### 3.5.2 User experience

To use security questions authentication, users can register at the security info registration <https://aka.ms/setupsecurityinfo>. The following screenshot shows how a user can add a security  authentication method.

<img src="./media/authentication/security-questions-1.png" width="400">

Then select the **security questions** authentication option.

<img src="./media/authentication/security-questions-2.png" width="400">

The user is asked to pick from a set of questions to prompt for and provide their own answers.

<img src="./media/authentication/security-questions-3.png" width="400">

During the sign-in, if a user selects **Can't access your account?**, or navigate to <https://aka.ms/sspr>. Then provide their UPN.

<img src="./media/authentication/security-questions-4.png" width="400">

After providing the UPN, the users is asked random questions from the pool of the security questions:


<img src="./media/authentication/security-questions-5.png" width="400">

### 3.6 Microsoft Authenticator

The [Microsoft Authenticator App](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-passwordless-phone) can be used to sign in to any Azure AD account without using a password on any platform or browser by getting a notification to their phone.

#### 3.6.2 User experience 

On the sign-in screen, user enters their username. A notification is sent to the Authenticator App via push notification system. Users view the notification, and if it's legitimate, select **Verify** to completed the sign-in. Otherwise, they can select **Deny**.

<img src="./media/authentication/number-matching-disabled.png" width="300">

##### 3.6.2.1 Number matching

When a user responds to an [MFA](https://docs.microsoft.com/azure/active-directory/authentication/how-to-mfa-number-match#multifactor-authentication), or [SSPR](https://docs.microsoft.com/azure/active-directory/authentication/howto-sspr-deployment) push notification using the Authenticator app, they'll be presented with [a number](https://docs.microsoft.com/azure/active-directory/authentication/how-to-mfa-number-match). They need to type that number into the app to complete the approval. 

The following screenshot shows the Number matching on both the sign-in page and the authenticator app.

<img src="./media/authentication/number-matching-enabled.png" width="600">


#### 3.6.2.2 Geographic location and app name

When a user receives a Passwordless phone sign-in or MFA push notification in the Authenticator app, they'll see the [name of the application](https://docs.microsoft.com/azure/active-directory/authentication/how-to-mfa-additional-context#enable-additional-context-in-the-portal) that requests the approval and the [location based](https://docs.microsoft.com/azure/active-directory/authentication/how-to-mfa-additional-context) on the IP address where the sign-in originated from.

The following screenshot shows the sign-in notification on the Microsoft Authenticator App with location and app name:

<img src="./media/authentication/auth-app-location.png" width="300">

### 3.7 SMS-based authentication

_Licensing_: P1 or P2

[SMS-based authentication](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-sms-signin) lets users sign-in without providing, or even knowing, their user name and password. After their account is created by an admin, they can enter their phone number at the sign-in prompt. They receive an authentication code via text message that they can provide to complete the sign-in. 

This authentication method simplifies access to applications and services, especially for Frontline workers.

#### 3.7.1 Admin experience 

There are three main steps to enable and use SMS-based authentication in your organization:

- [Enable the authentication](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-sms-signin#enable-the-sms-based-authentication-method) method policy.
- [Select users or groups](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-sms-signin#assign-the-authentication-method-to-users-and-groups) that can use the SMS-based authentication method.
- [Assign a phone number for each user](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-sms-signin#set-a-phone-number-for-user-accounts) account. The phone number **must be unique** in your tenant. A user can have a single phone number registered.

#### 3.7.2 User experience

To test the user account that's now enabled for SMS-based sign-in, complete the following steps:

1. Open a new InPrivate or Incognito web browser window to <https://myapps.microsoft.com>
1. At the sign-in prompt, enter the phone number associated with the user in the previous section, then select **Next**.
    
    <img src="./media/authentication/sms-based-sign-in-1.png" width="300">

1. A text message is sent to the phone number provided. To complete the sign-in process, enter the 6-digit code provided in the text message at the sign-in prompt. Then, select **Sign in**.
    
    <img src="./media/authentication/sms-based-sign-in-2.png" width="300">


### 3.8 Security key authentication (FIDO2)

[FIDO](https://docs.microsoft.com/azure/active-directory/authentication/concept-authentication-passwordless#fido2-security-keys) allows users and organizations to leverage the standard to sign in to their resources without a username or password using an external security key or a platform key built into a device. These FIDO2 **passkeys** (security keys) are typically USB devices, but could also use Bluetooth or NFC. With a hardware device that handles the authentication, the security of an account is increased as there's no password that could be exposed or guessed.

FIDO2 passkeys can be used to sign in to their Azure AD joined devices, or hybrid Azure AD joined Windows 10 devices and get single-sign on to their cloud and on-premises resources. macOS and Linux currently support only USB external devices. For more information, check out the [browser support of FIDO2 passwordless authentication](https://docs.microsoft.com/azure/active-directory/authentication/fido2-compatibility) article.

#### 3.8.1 Multi-device FIDO Credentials (passkeys)

If you are using Microsoft, Apple, or a Google device, your passkeys (security keys) can securely sync to your other devices of the same platform. So if you get a new device, just authenticate with your platform provider and all your credentials will automatically be ready to use.

For more information, check out the [Multi-Device FIDO Credentials](https://fidoalliance.org/white-paper-multi-device-fido-credentials/) White Paper. Some of the platforms are in Beta version and can't be used.

#### 3.8.2 Admin experience

Admins [enable FIDO passwordless security key sign-in](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-passwordless-security-key) on their Azure AD tenant. No need to install anything on any device or manage certificates. There are [some optional settings](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-passwordless-security-key#fido-security-key-optional-settings) for managing security keys per tenant. 

#### 3.8.3 User experience

Users can [register](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-passwordless-security-key#user-registration-and-management-of-fido2-security-keys) and then select a FIDO2 security key at the sign-in interface as their main means of authentication. The [Enable passwordless security key sign-in](https://docs.microsoft.com/azure/active-directory/authentication/howto-authentication-passwordless-security-key) tutorial shows how to sign-in using Windows 10 machine. The following example uses MacOs with an external FIDO2 USB device.

##### 3.8.3.1 FIDO enrollment user flow

To enroll a new FIDO security key sing-in, the user needs to follow there steps:

1. Browse to <https://myprofile.microsoft.com> and sign in (if not already) with their credentials, such as username and password, or phone sign-in.
1. From the menu, select **Security Info**. If prompted to Azure AD Multi-Factor Authentication, complete the MFA sign-in.
1. Select **+ Add sign-in method**.
    
    <img src="./media/authentication/fido-mac-add-sign-in-method.png" width="400">

1. From the avalible sign-in methods, select **Security Key**.
    
    <img src="./media/authentication/fido-mac-add-fido-1.png" width="400">   

1. Choose **USB device** or **NFC device**. In this example, we select USB device.

    <img src="./media/authentication/fido-mac-add-fido-2.png" width="400"> 

1. Have your key ready and choose **Next**.

    <img src="./media/authentication/fido-mac-add-fido-3.png" width="400"> 

1. A box will appear and ask the user to create/enter a **PIN** for your security key, then perform the required gesture for the key, either biometric or touch.

    <img src="./media/authentication/fido-mac-add-fido-4.png" width="400"> 

1. The user will be returned to the registration experience and asked to provide a meaningful name for the key so the user can identify which one if they have multiple. Select **Next**.

    <img src="./media/authentication/fido-mac-add-fido-5.png" width="400"> 

1. Select **Done** to complete the process.

##### 3.8.3.2 Sign-in with security key user flow

After a user has already provisioned their FIDO2 security key. They can choose to sign in on the web with their FIDO2 security key inside of a supported browser. The user goes through following steps:

1. Browse to <https://myapps.microsoft.com>, or other cloud app.
1. On the sign-in page, select  **Sing-in options**.

    <img src="./media/authentication/fido-mac-sign-in-1.png" width="400"> 

1. Select **Sign in with Windows Hello or a security key**.

    <img src="./media/authentication/fido-mac-sign-in-2.png" width="400"> 

1. Select **Allow** to _login.microsoft.com_ request.

    <img src="./media/authentication/fido-mac-sign-in-3.png" width="400"> 

1. This finalizes the sign-in flow. Now, you will be redirected back to the <https://myapps.microsoft.com>, or your cloud app.
