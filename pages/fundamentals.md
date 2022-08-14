# Azure Active directory fundamentals

## Users

### User management

[Add new users or delete existing users](https://docs.microsoft.com/azure/active-directory/fundamentals/add-users-azure-active-directory) from your Azure AD organization. Update the [user profile information](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-profile-azure-portal), including a profile picture, job-specific information.

### Reset a user's password

As an administrator, you can [reset a user's password](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-reset-password-azure-portal) if the password is forgotten, if the user gets locked out of a device, or if the user never received a password. 

### Restore or remove a recently deleted

After you delete a user, the account remains in a suspended state for 30 days. During that 30-day window, the user account can be restored, along with all its properties. After that 30-day window passes, the permanent deletion process is automatically started.

You can view your restorable users, [restore a deleted user, or permanently delete](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-restore) a user.



## Groups

### Group management

You can:

- [Create a security group and add members](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-groups-create-azure-portal). 
- [Add or remove group members](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-groups-members-azure-portal). 
- [Delete a group using and its members](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-groups-delete-group).
- [Edit your group information](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-groups-settings-azure-portal)
- [Add or remove group owners](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-accessmanagement-managing-group-owners)

### Group owners

Azure AD groups are [owned and managed by group owners](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-accessmanagement-managing-group-owners). Group owners can be users or service principals, and are able to manage the group including membership.

### Nested groups

You can [add an existing security group to another existing security group](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-groups-membership-azure-portal) (also known as nested groups), creating a member group (subgroup) and a parent group. The member group inherits the attributes and properties of the parent group, saving you configuration time.

### Self-service group membership

_Licensing_: P1 or P2

Users join [groups without being assigned](https://docs.microsoft.com/azure/active-directory/enterprise-users/groups-self-service-management). The group owner can let users find their own groups to join, instead of assigning them. The owner can also set up the group to automatically accept all users that join or to require approval.

### Dynamic groups

_Licensing_: P1 or P2

You can create attribute-based rules to enable dynamic membership for a group in Azure AD. Dynamic group membership adds and removes group members automatically using membership rules based on member attributes. 

When the attributes of a user or a device change, the system evaluates all dynamic group rules in a directory to see if the change would trigger any group adds or removes. If a user or device satisfies a rule on a group, they're added as a member of that group. If they no longer satisfy the rule, they're removed. You can't manually add or remove a member of a dynamic group.

For more information, check out the [Dynamic membership rules for groups](https://docs.microsoft.com/azure/active-directory/enterprise-users/groups-dynamic-membership) article.


## Permissions

### Default user permissions

In Azure AD, all users are granted a set of [default permissions](https://docs.microsoft.com/azure/active-directory/fundamentals/users-default-permissions). A user's access consists of the type of user, their role assignments, and their ownership of individual objects.

It's possible to [add restrictions to users' default permissions](https://docs.microsoft.com/azure/active-directory/fundamentals/users-default-permissions#restrict-member-users-default-permissions). You can use this feature if you don't want all users in the directory to have access to the Azure AD admin portal/directory.

### Assign roles

If one of your users needs permission to manage Azure AD resources, you must [assign](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-users-assign-role-azure-portal) them to a role that provides the permissions they need.

A common way to assign Azure AD roles to a user is on the Assigned roles page for a user. You can also configure the user eligibility to be elevated just-in-time into a role using Privileged Identity Management (PIM). For more information about how to use PIM, see [Privileged Identity Management](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/).

## Licensing

### Assign licenses to users

Many Azure AD and Microsoft 365 services require you to license each of your users or groups (and associated members) for that service. Only users with active licenses will be able to access and use the licensed Azure AD services for which that's true. Licenses are applied per tenant and do not transfer to other tenants. 

You can view your available service plans, including the individual licenses, check pending expiration dates, and view the number of available assignments. And assign licenses to users or groups.

For more information, check our the [Assign or remove licenses in the Azure Active Directory portal](https://docs.microsoft.com/azure/active-directory/fundamentals/license-users-groups) article.

### Group based licensing

_Licensing_: P1 or P2

You can assign one or more product [licenses to a group](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-licensing-whatis-azure-portal). Azure AD ensures that the licenses are assigned to all members of the group. Any new members who join the group are assigned the appropriate licenses. When they leave the group, those licenses are removed. 






## Security

### Security defaults

[Security defaults](https://docs.microsoft.com/azure/active-directory/fundamentals/concept-fundamentals-security-defaults) make it easier to help protect your organization from these identity-related attacks with preconfigured security settings:

- Requiring all users to register for Azure AD Multi-Factor Authentication.
- Requiring administrators to do multi-factor authentication.
- Requiring users to do multi-factor authentication when necessary.
- Blocking legacy authentication protocols.
- Protecting privileged activities like access to the Azure portal.

### Identity secure score

The [identity secure score](https://docs.microsoft.com/azure/active-directory/fundamentals/identity-secure-score) is percentage that functions as an indicator for how aligned you are with Microsoft's best practice recommendations for security. Each improvement action in identity secure score is tailored to your specific configuration.





## Multi-Factor Authentication

There are multiple ways to enable Azure AD Multi-Factor Authentication for your Azure Active Directory (AD) users based on the licenses that your organization owns.

TBD





## User experience

### Custom domain name

Every new Azure AD tenant comes with an initial domain name, `<domainname>.onmicrosoft.com`. You can't change or delete the initial domain name, but you can add your organization's names. Adding [custom domain names](https://docs.microsoft.com/azure/active-directory/fundamentals/add-custom-domain) helps you to create user names that are familiar to your users, such as alain@contoso.com.

### Company branding

_Licensing_: P1 or P2

The [company branding](https://docs.microsoft.comazure/active-directory/fundamentals/customize-branding) allows you to add your organization's logo and custom color schemes to provide a consistent look-and-feel on your Azure AD sign-in pages. Your sign-in pages appear when users sign in to your organization's web-based apps, such as Microsoft 365, which uses Azure AD as your identity provider.

### Privacy info

You can add [privacy-related info](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-properties-area) to an organization's Azure AD. The privacy info appears when users sign in to your organization's web-based apps, such as Microsoft 365, which uses Azure AD as your identity provider.

You can include:

- An email address for the person to contact for technical support within your organization
- An email address for the person to contact for inquiries about personal data privacy. 
- A link to your organization's document that describes how your organization handles both internal and external guest's data privacy


### Stay signed in (Keep me signed in)

_Licensing_: Basic, P1 or P2

The [keep me signed in (KMSI)](https://docs.microsoft.com/azure/active-directory/fundamentals/keep-me-signed-in) displays a Stay signed in? prompt after a user successfully signs in. If a user answers Yes to this prompt, the keep me signed in service gives them a persistent refresh token. For federated tenants, the prompt will show after the user successfully authenticates with the federated identity service.




## Custom attributes

### Custom security attributes

_Licensing_: [P1 or P2](https://docs.microsoft.com/azure/active-directory/fundamentals/custom-security-attributes-overview#known-issues)

[Custom security attributes](https://docs.microsoft.com/azure/active-directory/fundamentals/custom-security-attributes-overview) in Azure AD are business-specific attributes (key-value pairs) that you can define and assign to Azure AD objects, such as users and apps. These attributes can be used to store information, categorize objects, or enforce fine-grained access control over specific Azure resources. Custom security attributes can be used with Azure attribute-based access control (Azure ABAC).

### Directory schema extension attributes (custom attributes)

[Directory schema extension attributes](https://docs.microsoft.com/azure/active-directory/develop/active-directory-schema-extensions) provide a way to store additional data in Azure Active Directory on user objects and other directory objects such as groups, tenant details, service principals. Only extension attributes on user objects can be used for emitting claims to applications. This article describes how to use directory schema extension attributes for sending user data to applications in token claims.


## Next topic

[Application management](./manage-apps.md)