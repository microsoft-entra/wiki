# Microsoft Defender for Identity

[Microsoft Defender for Identity](https://docs.microsoft.com/defender-for-identity/what-is) (formerly Azure Advanced Threat Protection, also known as Azure ATP) is a cloud-based security solution that leverages your **on-premises Active Directory** signals to identify, detect, and investigate advanced threats, compromised identities, and malicious insider actions directed at your organization.

It uses machine learning and behavioral analytics to identify attacks across your on-premises network along with detecting and proactively preventing user sign-in risks associated with cloud identities.

Defender for Identity protects your on-premises Active Directory users and/or users synced to your Azure Active Directory (Azure AD). **To protect an environment made up of only Azure AD users**, see [Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/identity-protection/overview-identity-protection).

The following diagram illustrates the baseline architecture for Defender for Identity:

![Diagram illustrates the baseline architecture for Defender for Identity](https://docs.microsoft.com/microsoft-365/media/defender/m365-defender-identity-architecture.png?view=o365-worldwide)

## Deployment

To [Set up the Defender](https://docs.microsoft.com/microsoft-365/security/defender/eval-defender-identity-enable-eval?view=o365-worldwide):

1. Create the Defender for Identity instance
1. **Install the sensors on AD domain controllers** parse logs and network traffic and send them to Microsoft Defender for Identity for analysis and reporting.
1. [Optionally] **Install the sensors on Active Directory Federation Services (AD FS)** when Azure AD is configured to use federated authentication.