# Conditional Access

[Conditional Access](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) brings signals together, to make decisions, and enforce organizational policies. 

## Access policy components

Conditional Access policies at their simplest are if-then statements, if a user wants to access a resource, then they must complete an action. Example: A payroll manager wants to access the payroll application and is required to do multi-factor authentication to access it. This section describes the component of an access policy.

### 1. Assignments

The assignments portion controls the who, what, and where of the Conditional Access policy. You can choose from one of the following.

#### 1.1 Users and groups

- [Users and groups](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-users-groups). You can choose "None", "All users", "Select users and groups", "Gust and external users", and "Directory roles".
- [Workload identities](https://docs.microsoft.com/azure/active-directory/conditional-access/workload-identity). A [workload identity](https://docs.microsoft.com/azure/active-directory/develop/workload-identities-overview) is an identity that allows an application or service principal access to resources, sometimes in the context of a user. Check also, [Securing workload identities with PIM](https://docs.microsoft.com/azure/active-directory/identity-protection/concept-workload-identity-risk)
  - _Licensing_: P2

#### 1.2 Cloud apps or actions

- [Cloud apps](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-cloud-apps). The *cloud apps* include built-in Microsoft applications and any [Azure AD integrated applications including gallery](https://docs.microsoft.com/azure/active-directory/manage-apps/what-is-application-management), non-gallery, and applications published through [Application Proxy](https://docs.microsoft.com/azure/active-directory/app-proxy/what-is-application-proxy). 
- [User action](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-cloud-apps#user-actions). [Tasks that can be performed by a user](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-cloud-apps#user-actions), such as register security information or register or join devices.

#### 1.3 Conditions

Within a Conditional Access policy, an administrator can make use of the following signals:

- [Sign-in risk](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-conditions#sign-in-risk) -  With [Identity Protection](https://docs.microsoft.com/azure/active-directory/identity-protection/overview-identity-protection), sign-in risk can be evaluated as part of a Conditional Access policy. Sign-in risk represents the probability that a given authentication request isn't authorized by the identity owner.
  - _Licensing_: P2
- [User risk](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-conditions#user-risk) -  With [Identity Protection](https://docs.microsoft.com/azure/active-directory/identity-protection/overview-identity-protection), user risk can be evaluated as part of a Conditional Access policy. User risk represents the probability that a given identity or account is compromised.
  - _Licensing_: P2
- [Device platforms](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-conditions#device-platforms) - The device platform is characterized by the operating system that runs on a device. Azure AD identifies the platform by using information provided by the device, such as user agent strings. Since user agent strings can be modified, this information is unverified. Device platform should be used in concert with Microsoft Intune device compliance policies or as part of a block statement.
- [Locations](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-conditions#locations) - organizations can choose to include or exclude locations. These named locations may include the public IPv4 network information, country or region, or even unknown areas that don't map to specific countries or regions. Only IP ranges can be marked as a trusted location.
- [Client apps](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-conditions#client-apps) - the software the user is employing to access the cloud app. For example, 'Browser', and 'Mobile apps and desktop clients'. 
- [Filter for devices](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-conditions#client-apps) - organizations can choose to include or exclude devices based on a filter using a rule expression on device properties. The rule expression for filter for devices can be authored using rule builder or rule syntax. 

### 2. Access controls

The access controls portion of the Conditional Access policy controls how a policy is enforced.

#### 2.1 Grant

The [Grant](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-grant) provides administrators with a means of policy enforcement where they can block or grant access. You can choose from:

- **Block access** - Block access does just that, it will block access under the specified assignments. The block control is powerful and should be wielded with the appropriate knowledge.
- **Grant access** - When granted, the user may be prompted to complete more grant control requirements:

    - Require [Multi-factor authentication](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-grant#require-multi-factor-authentication). It requires users to perform Azure AD Multi-factor Authentication.
    - Require the [Device to be marked as compliant](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-grant#require-device-to-be-marked-as-compliant). Organizations that have deployed Intune can use the information returned from their devices to identify devices that meet specific policy compliance requirements. Intune sends compliance information to Azure AD so Conditional Access can decide to grant or block access to resources.
    - Require the [Hybrid Azure AD joined device](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-grant#require-hybrid-azure-ad-joined-device). Organizations can require that devices are [hybrid Azure AD joined](https://docs.microsoft.com/azure/active-directory/devices/howto-hybrid-azure-ad-join).
    - Require [Approved client app](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-grant#require-approved-client-app). It requires that an [Intune app protection policies](https://docs.microsoft.com/mem/intune/apps/app-protection-policy) approved client app is used.
    - Require [App protection policy](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-grant#require-app-protection-policy). Requires that an [Intune app protection policy](https://docs.microsoft.com/mem/intune/apps/app-protection-policy) is present on the client app before access is available to the selected cloud apps.
    - Require [Require password change](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-grant#require-password-change). Have the user securely change a password by using Azure AD [self-service password reset](https://docs.microsoft.com/azure/active-directory/authentication/tutorial-enable-sspr).
    - Require [Terms of use](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-grant#terms-of-use). User's acknowledgment of terms of use as a condition of accessing the resources that the policy protects.

### 3.1 Session

Within a Conditional Access policy, an administrator can make use of [session controls](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-session) to enable limited experiences within specific cloud applications. You can select the following options:

- [Use app enforced restrictions](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-session#application-enforced-restrictions) - passes device information to the selected cloud apps to allow control of experience granting full or limited access. Currently works with Exchange Online and SharePoint Online only.

- [Use Conditional Access App Control](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-session#conditional-access-application-control) - uses signals from Microsoft Defender for Cloud Apps to do things like: Block download, cut, copy, and print of sensitive documents. Monitor risky session behavior. Require labeling of sensitive files.
- [Sign-in frequency](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-session#sign-in-frequency) - tht ability to change the default sign in frequency for modern authentication.
- [Persistent browser session](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-session#persistent-browser-session) - allows users to remain signed in after closing and reopening their browser window. Persistent Browser Session configuration in Azure AD Conditional Access will overwrite the “Stay signed in?” setting in the [company branding](https://docs.microsoft.com/azure/active-directory/fundamentals/customize-branding) pane in the Azure portal for the same user if you have configured both policies.
- [Customize continuous access evaluation](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-session#customize-continuous-access-evaluation) - allows access tokens to be revoked based on critical events and policy evaluation in real time rather than relying on token expiration based on lifetime. For example, when the network location is changed, or user has been disabled.
- [Disable resilience defaults](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-session#disable-resilience-defaults-preview) - during an outage, Azure AD will extend access to existing sessions while enforcing Conditional Access policies. If a policy can't be evaluated, access is determined by resilience settings.

### 4. Enable policy

Administrators can configure the policy mode to one of the following:

- **On** - the access policy is active
- **Off** - the access policy will not run.
- **Report-only** - with the [report-only mode](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-report-only) Conditional Access policy state that allows administrators to evaluate the impact of Conditional Access policies before enabling them in their environment. With the report only mode, policies are evaluated but not enforced. Results are logged in the **Conditional Access** and **Report-only** tabs of the **Sign-in log** details. Customers with an Azure Monitor subscription can monitor the impact of their Conditional Access policies using the Conditional Access insights workbook.

## Conditional Access templates

[Conditional Access templates](https://docs.microsoft.com/azure/active-directory/conditional-access/concept-conditional-access-policy-common#conditional-access-templates-preview) are designed to provide a convenient method to deploy new policies aligned with Microsoft recommendations. These templates are designed to provide maximum protection aligned with commonly used policies across various customer types and locations.

## What If tool

The Conditional Access [What If policy tool](https://docs.microsoft.com/azure/active-directory/conditional-access/what-if-tool) allows you to understand the impact of your Conditional Access policies on your environment. Instead of test driving your policies by performing multiple sign-ins manually, this tool enables you to evaluate a simulated sign-in of a user. The simulation estimates the impact this sign-in has on your policies and generates a simulation report. The report does not only list the applied Conditional Access policies but also classic policies if they exist.
