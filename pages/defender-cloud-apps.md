# Microsoft Defender for Cloud Apps

> Draft document!

[Microsoft Defender for Cloud Apps](https://docs.microsoft.com/defender-cloud-apps/what-is-defender-for-cloud-apps) (formerly called 'Microsoft Cloud App Security') is a Cloud Access Security Broker (CASB) that supports various deployment modes including log collection, API connectors, and reverse proxy. It provides rich visibility, control over data travel, and sophisticated analytics to identify and combat cyberthreats across all your Microsoft and third-party cloud services.

For more information:

- [Getting Started with Microsoft Defender for Cloud Apps by Andy Malone
](https://www.youtube.com/watch?v=FbKkh9-Iir8)
- [Microsoft Defender for Cloud Apps Security: Overview](https://www.youtube.com/watch?v=iAs_Jn4dkVY)

## 1. Cloud Discovery

[Cloud Discovery](https://docs.microsoft.com/defender-cloud-apps/set-up-cloud-discovery) analyzes your traffic logs against the Microsoft Defender for Cloud Apps catalog of over 31,000 cloud apps. The apps are ranked and scored based on more than 90 risk factors to provide you with ongoing visibility into cloud use, Shadow IT, and the risk Shadow IT poses into your organization.

### 1.1 Reports

You can generate the following types of reports:

#### 1.1.1 Snapshot reports

Provides ad-hoc visibility on a set on traffic logs you manually upload from your firewalls and proxies. It's important to upload a log manually and let Microsoft Defender for Cloud Apps parse it before trying to use the automatic log collector. If you don't have a log yet and you want to see an example of what your log should look like, download a sample log file.

#### 1.1.2 Continuous reports

[Continuous reports](https://docs.microsoft.com/defender-cloud-apps/set-up-cloud-discovery#snapshot-and-continuous-risk-assessment-reports) can be created by connecting in the following ways:

- [Microsoft Defender for Endpoint integration](https://docs.microsoft.com/defender-cloud-apps/mde-integration): Defender for Cloud Apps integrates with Defender for Endpoint natively, to simplify rollout of Cloud Discovery, extend Cloud Discovery capabilities beyond your corporate network, and enable machine-based investigation. Defender for Cloud Apps uses the traffic information collected by Defender for Endpoint about the cloud apps and services being accessed from the devices.
- [Log collector](https://docs.microsoft.com/defender-cloud-apps/discovery-docker): enable you to easily automate log upload from your network. The log collector runs on your network and receives logs over Syslog or FTP from [supported firewalls and proxies
](https://docs.microsoft.com/defender-cloud-apps/set-up-cloud-discovery#supported-firewalls-and-proxies-). If your log isn't supported, use [a custom log parser](https://docs.microsoft.com/defender-cloud-apps/custom-log-parser)
- **Secure Web Gateway (SWG)**: the following SWGs provide seamless deployment of Cloud Discovery, automatic blocking of unsanctioned apps, and risk assessment directly in the SWG's portal: [Zscaler](https://docs.microsoft.com/defender-cloud-apps/zscaler-integration), [iboss](https://docs.microsoft.com/defender-cloud-apps/iboss-integration), [Corrata](https://docs.microsoft.com/defender-cloud-apps/corrata-integration), [Menlo](https://docs.microsoft.com/defender-cloud-apps/menlo-integration)
- [Cloud Discovery API](https://docs.microsoft.com/defender-cloud-apps/api-discovery): Use the Defender for Cloud Apps Cloud Discovery API to automate traffic log upload and get automated Cloud Discovery report and risk assessment. You can also use the API to [generate block scripts](https://docs.microsoft.com/defender-cloud-apps/api-discovery-script) and streamline app controls directly to your network appliance.

### 1.2 Cloud Discovery enrichment

Cloud Discovery data can be [enriched with Azure AD username data](https://docs.microsoft.com/defender-cloud-apps/cloud-discovery-aad-enrichment). When you enable this feature, the username, received in discovery traffic logs, is matched and replaced by the Azure AD username. Cloud Discovery enrichment enables the following features:

- You can investigate Shadow IT usage by Azure Active Directory user. The user will be shown with its UPN.
- You can correlate the Discovered cloud app use with the API collected activities.
- You can then create custom logs based on Azure AD user groups. For example, a Shadow IT report for a specific Marketing department.

### 1.3 Data anonymization

Cloud Discovery [data anonymization](https://docs.microsoft.com/defender-cloud-apps/cloud-discovery-anonymizer) enables you to protect user privacy. Once the data log is uploaded to the Microsoft Defender for Cloud Apps portal, the log is sanitized and all username information is replaced with encrypted usernames. This way, all cloud activities are kept anonymous. When necessary, for a specific security investigation (for example, a security breach or suspicious user activity), admins can resolve the real username. 


## 2. Connected apps

[App connectors](https://docs.microsoft.com/defender-cloud-apps/enable-instant-visibility-protection-and-governance-actions-for-your-apps) use the APIs of app providers to enable greater visibility and control by Microsoft Defender for Cloud Apps over the apps you connect to.

Each service has its own framework and API limitations such as throttling, API limits, dynamic time-shifting API windows, and others. Microsoft Defender for Cloud Apps worked with the services to optimize the usage of the APIs and to provide the best performance. For more information, check out the [Connect apps](https://docs.microsoft.com/defender-cloud-apps/enable-instant-visibility-protection-and-governance-actions-for-your-apps) article. 

The following apps are supported: [Atlassian](https://docs.microsoft.com/defender-cloud-apps/connect-atlassian), [Azure](https://docs.microsoft.com/defender-cloud-apps/connect-azure), [AWS](https://docs.microsoft.com/defender-cloud-apps/connect-aws), [Box](https://docs.microsoft.com/defender-cloud-apps/connect-box), [DocuSign](https://docs.microsoft.com/defender-cloud-apps/connect-docusign), [Dropbox](https://docs.microsoft.com/defender-cloud-apps/connect-dropbox), [Egnyte](https://docs.microsoft.com/defender-cloud-apps/connect-egnyte), [GitHub](https://docs.microsoft.com/defender-cloud-apps/connect-github-ec),[Google Workspace](https://docs.microsoft.com/defender-cloud-apps/connect-google-workspace), [Google Cloud Platform (GCP)](https://docs.microsoft.com/defender-cloud-apps/connect-google-gcp), [NetDocuments](https://docs.microsoft.com/defender-cloud-apps/connect-netdocuments-to-microsoft-defender-for-cloud-apps), [Office 365](https://docs.microsoft.com/defender-cloud-apps/connect-office-365), [Okta](https://docs.microsoft.com/defender-cloud-apps/connect-okta), [OneLogin](https://docs.microsoft.com/defender-cloud-apps/connect-onelogin), [Salesforce](https://docs.microsoft.com/defender-cloud-apps/connect-salesforce), [ServiceNow](https://docs.microsoft.com/defender-cloud-apps/connect-servicenow), [Slack](https://docs.microsoft.com/defender-cloud-apps/connect-slack), [Smartsheet](https://docs.microsoft.com/defender-cloud-apps/connect-smartsheet), [Cisco Webex Teams](https://docs.microsoft.com/defender-cloud-apps/connect-webex), [Workday](https://docs.microsoft.com/defender-cloud-apps/connect-workday), [Zendesk](https://docs.microsoft.com/defender-cloud-apps/connect-zendesk). 

> TIP: To get started, configure the [Azure](https://docs.microsoft.com/defender-cloud-apps/connect-azure) and [Office 365](https://docs.microsoft.com/defender-cloud-apps/connect-office-365).

## 3. Conditional Access App Control

It's often not enough to know what's happening in your cloud environment after the fact. You want to stop breaches and leaks in real time, before employees intentionally or inadvertently put your data and your organization at risk. 

[Conditional Access App Control](https://docs.microsoft.com/defender-cloud-apps/proxy-intro-aad#how-it-works) uses a **reverse proxy** architecture, instead of directly access to the app. When a session is protected by proxy, all the relevant URLs and cookies are replaced by Defender for Cloud Apps. For example, if the app returns a page with links whose domains end with `myapp.com`, the link's domain is suffixed with something like `myapp.com.mcas.ms`. This method doesn't require you to install anything on the device making it ideal when monitoring or controlling sessions from unmanaged devices or partner users.

With the access and session policies, you can for example:

- You can block the download, cut, copy, and print of sensitive documents on, for example, unmanaged devices.
- Require multi-factor authentication on download of a highly confidential file.
- Prevent upload of unlabeled files. Before a sensitive file is uploaded, distributed, and used by others, it's important to make sure that the sensitive file has the label defined by your organization's policy. You can ensure that unlabeled files with sensitive content are blocked from being uploaded until the user classifies the content.

## 4. Investigate

TBD



