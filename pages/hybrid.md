# Azure AD Connect

Azure AD Connect allows organizations to sync their users and groups to Azure AD.

> Before you start reading this article, consider the cloud-managed solution [Azure AD Connect **cloud** sync](./cloud-sync.md). It's the newest and recommended solution for Active Directory sync to the cloud.

## 1. Azure AD Connect V2.0

Major changes in the v2.0 you should consider:

- It uses [SQL Server 2019 LocalDB](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-azure-ad-connect-v2#sql-server-2019-localdb)
- [Requires Windows Server 2016 or newer](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-azure-ad-connect-v2#windows-server-2012-and-windows-server-2012-r2-are-no-longer-supported) as a server operating system
- [Requires PowerShell 5.0](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-azure-ad-connect-v2#powershell-50)
- The V2.0 release doesn't contain any new functionality. This release only contains updates of some of the foundational components on Azure AD Connect. However, later releases of Azure AD Connect V2 may contain new functionality.
- All Azure AD Connect V1 versions will be retired on 31 August, 2022
- [Upgrades from any previous version](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-upgrade-previous-version) of Azure AD Connect to Azure AD Connect V2 is supported. However if you have enabled the auto-upgrade feature, it will be upgraded to the latest release.

## 2. Azure AD Connect sync

The [Azure AD Connect sync](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sync-whatis) is a main component of Azure AD Connect. It takes care of all the operations that are related to synchronize identity data between your on-premises environment and Azure AD. 

The sync service consists of two components: 

- The on-premises component named [**Azure AD Connect sync**](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-syncservice-features), also called sync engine. Note, the [Microsoft Azure AD Sync synchronization service (ADSync)](https://docs.microsoft.com/azure/active-directory/hybrid/concept-adsync-service-account) runs on a server in your on-premises environment.
- The service residing in Azure AD also known as **Azure AD Connect sync service**.

Azure AD Connect sync is the successor of DirSync, Azure AD Sync, and Forefront Identity Manager with the Azure Active Directory Connector configured.

### 2.1 Service account

Azure AD Connect installs an on-premises service which orchestrates synchronization between AD and Azure AD. The Microsoft Azure AD Sync synchronization service (ADSync) runs on a server in your on-premises environment. The [credentials for the service](https://docs.microsoft.com/azure/active-directory/hybrid/concept-adsync-service-account) are set by default in the Express installations but may be customized to meet your organizational security requirements. 

### 2.2 Configuration

The Azure AD Connect sync [settings are configured by the Azure Active Directory Module](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-syncservice-features) for Windows PowerShell. Download and install it separately from Azure AD Connect. 

#### 2.2.1 Synchronization Service Manager UI

The [Synchronization Service Manager UI](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sync-service-manager-ui) is used to configure more advanced aspects of the sync engine and to see the operational aspects of the service.

## 2.3 Password hash synchronization

[Password hash synchronization](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-phs) is one of the sign-in methods used to accomplish hybrid identity. Azure AD Connect synchronizes a hash, of the hash, of a user's password from an on-premises AD instance to a cloud-based Azure AD instance.

Users sign in to the service by using the same password you use to sign in to your on-premises AD instance. If the on-premises AD isn't available, users can still access cloud only service, such as SharePoint online.

Password Hash Sync also enables [leaked credential detection](https://docs.microsoft.com/azure/active-directory/identity-protection/concept-identity-protection-risks#user-linked-detections) for your hybrid accounts. 

### 2.3.1 Selective password hash synchronization

If you'd like to have a subset of users excluded from synchronizing their password hash to Azure AD, you can configure [selective password hash synchronization](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-selective-password-hash-synchronization).

### 2.3.2 Password policy considerations

There are two types of password policies that are [affected](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-password-hash-synchronization#password-policy-considerations) by enabling password hash synchronization:

- [Password complexity policy](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-password-hash-synchronization#password-complexity-policy) - the password complexity policies in your on-premises AD instance override complexity policies in the cloud for synchronized users. You can use all of the valid passwords from your on-premises AD instance to access Azure AD services.
- [Password expiration policy](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-password-hash-synchronization#password-expiration-policy) default the cloud account password is set to Never Expire `"passwordPolicies": "DisablePasswordExpiration"`.  Users can continue to sign in to your cloud services by using a synchronized password that is expired in the on-premises environment. User's cloud password is updated the next time they change the password in the on-premises environment.

    Administrators can force users to comply with your Azure AD password expiration policy by enabling the `EnforceCloudPasswordPolicyForPasswordSyncedUsers` feature of the Azure AD Connect sync. For more information, check out the [Configuration](#22-configuration) section of this article.

## 3. Pass-through authentication

[Pass-through Authentication](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) allows your users to sign in to both on-premises and cloud-based applications using the same passwords. When users sign in using Azure AD, the users' passwords are validated directly against your on-premises AD. 

For more information, check out the following articles:

- [How Pass-through Authentication works](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-how-it-works)
- [Pass-through Authentication security deep dive](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-security-deep-dive)
- [Limitations an unsupported scenarios](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-current-limitations)
- [User Privacy and Azure Active Directory Pass-through Authentication](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta-user-privacy)

## 4. Federation integration

Admins can [federate](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-fed) on-premises environment with Azure AD and use this federation for authentication and authorization. This sign-in method ensures that all user authentication occurs on-premises. This method allows administrators to implement more rigorous levels of access control. Federation with AD FS and PingFederate is available.

For more information, check out the following articles:

- [What is federation with Azure AD?](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-fed)
- [Azure AD Connect and federation](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-fed-whatis)
- [Azure AD federation compatibility list](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-fed-compatibility)

## 5. Choose the right authentication method

Choosing the correct authentication method is a crucial first decision in setting up an Azure AD hybrid identity solution. Implement the authentication method that is configured by using Azure AD Connect, which also provisions users in the cloud. Check out the [Choose the right authentication method for your Azure Active Directory hybrid identity solution](https://docs.microsoft.com/azure/active-directory/hybrid/choose-ad-authn) article.

## 6. Single Sign-On

With Single Sign-On users don't need to type in their passwords to sign in **to Azure AD**, and usually, even type in their usernames. It provides your users easy access to your **cloud-based applications** without needing any additional on-premises components.

For Windows 10, Windows Server 2016 and later versions, **it’s recommended** to use SSO via [primary refresh token (PRT)](https://docs.microsoft.com/azure/active-directory/devices/concept-primary-refresh-token). For Windows 7 and Windows 8.1, it’s recommended to use [Seamless SSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) (needs the device to be domain-joined). Read more about [SSO via primary refresh token vs. Seamless SSO](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)

### 6.1 Seamless SSO solution

[Azure AD Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso) (Azure AD Seamless SSO) automatically signs users in when they are on their corporate devices connected to your corporate network. When enabled, users don't need to type in their passwords to sign in **to Azure AD**, and usually, even type in their usernames. This feature provides your users easy access to your **cloud-based applications** without needing any additional on-premises components.

Seamless SSO can be combined with either the [Password Hash Synchronization](#23-password-hash-synchronization) or [Pass-through Authentication](#3-pass-through-authentication) sign-in methods. Seamless SSO is not applicable to Active Directory Federation Services (ADFS).

For more information about Azure AD Seamless SSO, check out the following articles:

- [Azure Active Directory Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso)
- [Seamless Single Sign-On technical deep dive](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso-how-it-works)
- [User Privacy and Azure AD Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso-user-privacy)
- [Deploy Seamless Single Sign-On](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso-quick-start)
- [Seamless Single Sign-On: Frequently asked questions](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-sso-faq)

### 6.2 Primary Refresh Token solution

SSO via primary refresh token works once devices are registered with Azure AD. The PRT is issued during user authentication on a Windows 10 or newer device in following scenarios:

- [Hybrid Azure AD joined](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid) devices  
- [Azure AD joined](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join) devices
-  Personal registered devices via [Azure AD registered](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-register) devices

For more information on how SSO works with PRT, check out the [What is a Primary Refresh Token](https://docs.microsoft.com/azure/active-directory/devices/concept-primary-refresh-token) article.

## 7. Staged Rollout

If you have an Azure AD tenant with [federated domains](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-fed) (for example, using AD-FS), [Staged Rollout](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-staged-rollout) allows you to selectively test groups of users with cloud authentication such as, [Password hash synchronization (PHS)](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-phs), and [Pass-through authentication (PTA)](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-pta) before cutting over your entire domains.

## 8. Health Monitoring

_Licensing_: P1

[Azure AD Connect Health](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-azure-ad-connect) provides monitoring of the on-premises identity infrastructure. The information is presented in the [Azure AD Connect Health porta](https://aka.ms/aadconnecthealth). Use the Azure AD Connect Health portal to view alerts, performance monitoring, usage analytics, and other information.

It also supports monitoring the AD FS proxy or web application proxy servers that provide authentication support for extranet access.