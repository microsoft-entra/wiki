# Device identity

This a draft version!!!

A device identity is an object in Azure AD similar to users, groups, or applications. It gives admins information they can use when making access or configuration decisions. For example, [device-based Conditional Access policies](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-grant) and Mobile Device Management with [Microsoft Endpoint Manager](https://docs.microsoft.com/mem/endpoint-manager-overview).


|Scenario   | Operating System| Provisioning| Sign in options| Device management| 
|---------|---------|---------|---------|---------|
| [Azure AD registration](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-register)| Windows 10 or newer, iOS, Android, and macOS | <ul><li>**Windows** 10 or newer: settings</li><li>**iOS/Android**: Company Portal or Microsoft Authenticator app</li><li>**macOS:** Company Portal</li></ul>| <ul><li>End-user local credentials</li><li>Password</li><li>Windows Hello</li><li>PIN</li><li>Biometrics or pattern for other devices</li></ul>| <ul><li>Mobile Device Management (example: Microsoft Intune)</li><li>Mobile Application Management</li></ul>|  
| [Azure AD join](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join)| Windows 11, or 10 | <ul><li>Self-service: Windows Out of Box Experience (OOBE) or Settings</li><li>Bulk enrollment</li><li>Windows Autopilot</li></ul>|Organizational accounts using: <ul><li>Password</li><li>Windows Hello for Business</li><li>FIDO2.0 security keys</li></ul>| <ul><li>Mobile Device Management (example: Microsoft Intune)</li><li>[Configuration Manager with Microsoft Intune](https://docs.microsoft.com/mem/configmgr/comanage/overview)</li></ul>|  
| [Hybrid Azure AD join](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-join-hybrid)| Windows 11, 10, or 8.1 <br/> Windows Server (1)| See the list below (2)| Organizational accounts using: <ul><li>Password</li><li>Windows Hello for Business for Win10 and above</li></ul>| <ul><li>[Group Policy](https://docs.microsoft.com/mem/configmgr/comanage/faq#my-environment-has-too-many-group-policy-objects-and-legacy-authenticated-apps--do-i-have-to-use-hybrid-azure-ad-)</li><li>[Configuration Manager with Microsoft Intune](https://docs.microsoft.com/mem/configmgr/comanage/overview)</li></ul>| 

Appendix:

1. Windows Server 2008/R2, 2012/R2, 2016, 2019 and 2022
1. Provisioning for Hybrid Azure AD join:
    - Windows 11, Windows 10, Windows Server 2016/2019/2022
    - Domain join by IT and autojoin via Azure AD Connect or ADFS config
    - Domain join by Windows Autopilot and autojoin via Azure AD Connect or ADFS config
    - Windows 8.1, Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2 - Require MSI

## 1. Device identity scenarios

There are three ways to get a device identity as described in this section.

### 1.1 Azure AD registration

The goal of [Azure AD registered devices](https://docs.microsoft.com/azure/active-directory/devices/concept-azure-ad-register) (also known as Workplace joined devices) is to provide your users with support for bring your own device (BYOD) or mobile device scenarios. In these scenarios, a user can access your organization’s resources using **personal devices**.

- **Sign-in** - Azure AD registered devices are signed in to using a local account like a Microsoft account on a Windows 10 or newer device. These devices have an Azure AD account for access to organizational resources.
- **Access control** - Access to resources in the organization can be limited based on that Azure AD account and Conditional Access policies applied to the device identity.
- **Device management** - you can control the devices using Mobile Device Management (MDM) tools like Microsoft Intune. MDM provides a means to enforce organization-required configurations like requiring storage to be encrypted, password complexity, and security software kept updated.

### 1.2 Azure AD join

### 1.3 Hybrid Azure AD join