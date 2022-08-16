# App provisioning

App provisioning allows you to automatically create, update and remove user and groups in applications that users need access to. 

## 1. Apps and platforms

## 1.1 Pre-integrated applications (gallery apps)

Most cloud and SaaS applications (pre-integrated apps) store the users role and permissions in the user's own local user profile store, and presence of such a user record in the user's local store is required for single sign-on and access to work. These apps use SCIM based user management APIs for provisioning. 

Learn how to [mange user account provisioning for enterprise apps in the Azure portal](https://docs.microsoft.com/azure/active-directory/app-provisioning/configure-automatic-user-provisioning-portal). You should start by finding the provisioning setup tutorial specific to your application in the [List of tutorials on how to integrate SaaS apps with Azure AD](https://docs.microsoft.com/azure/active-directory/saas-apps/tutorial-list)

## 1.2 Cloud apps that support SCIM

_Licensing_: P2

For apps that are publicly available, you can use the System for Cross-Domain Identity Management (SCIM) user management API to enable automatic [provisioning of users and groups](https://docs.microsoft.com/azure/active-directory/app-provisioning/use-scim-to-provision-users-and-groups) between your application and Azure AD.

SCIM is a standardized definition of two endpoints: a `/Users` endpoint and a `/Groups` endpoint. It uses common REST verbs to create, update, and delete objects, and a pre-defined schema for common attributes like group name, username, first name, last name and email. To manage the users' lifecycle in your application's identity store, Azure AD sends HTTP messages to apps' SCIM 2.0 endpoints. 

Note, that app must be added as a non-gallery app. For more information, check out the [get started](https://docs.microsoft.com/azure/active-directory/app-provisioning/use-scim-to-provision-users-and-groups#getting-started) section or the Tutorial: Develop and plan provisioning for a SCIM endpoint in Azure Active Directory article.

## 1.3 On-premises application provisioning

_Licensing_: P1 or P2

Azure AD also supports provisioning users into applications hosted on-premises or in a virtual machine, without having to open up any firewalls. Use the **Azure AD Provisioning agent** to directly connect with your app and automate provisioning and deprovisioning for the following applications:

- [Applications that support SCIM](https://docs.microsoft.com/azure/active-directory/app-provisioning/on-premises-scim-provisioning) - Azure AD Provisioning agent sends HTTP requests to apps that deployed in your corporate network without the need to expose the app to the internet.
- [Applications that rely on an LDAP](https://docs.microsoft.com/azure/active-directory/app-provisioning/on-premises-ldap-connector-configure)
- [Applications that stores the identities in an SQL database](https://docs.microsoft.com/azure/active-directory/app-provisioning/tutorial-ecma-sql-connector)

## 2. Attribute-mappings

Azure portal controls its attribute values through attribute-mappings. There's a pre-configured set of attributes and attribute-mappings between Azure AD user objects and each SaaS app's user objects. Some apps manage other types of objects along with Users, such as Groups.

You can [customize](https://docs.microsoft.com/azure/active-directory/app-provisioning/customize-application-attributes) the default attribute-mappings according to your business needs. So, you can change or delete existing attribute-mappings, or create new attribute-mappings.

For SCIM applications, check out the [Develop and plan provisioning for a SCIM endpoint](https://docs.microsoft.com/azure/active-directory/app-provisioning/use-scim-to-provision-users-and-groups#design-your-user-and-group-schema) article.

## 3. Scope

You can choose to "sync all users and groups" in Azure aD, or "sync assigned users and groups" which syncs only those that are assigned to the application.

The [scoping filter](https://docs.microsoft.com/azure/active-directory/app-provisioning/define-conditional-rules-for-provisioning-user-accounts) allows the Azure AD provisioning service to include or exclude any users who have an attribute that matches a specific value. For example, when provisioning users from Azure AD to a SaaS application used by a sales team, you can specify that only users with a "Department" attribute of "Sales" should be in scope for provisioning.

## 4. Check the status of user provisioning

The Azure AD provisioning service runs an initial provisioning cycle against the source system and target system, followed by periodic incremental cycles. When you configure provisioning for an app, you can [check the current status of the provisioning service](https://docs.microsoft.com/azure/active-directory/app-provisioning/application-provisioning-when-will-provisioning-finish-specific-user) and see when a user will be able to access an app.

## 5. Accidental deletions prevention

The Azure AD provisioning service includes a feature to help [avoid accidental deletions](https://docs.microsoft.com/azure/active-directory/app-provisioning/accidental-deletions). This feature ensures that users aren't disabled or deleted in an application unexpectedly.

The feature lets you specify a deletion threshold, above which an admin needs to explicitly choose to allow the deletions to be processed.