# Privilege identity management

Privileged Identity Management provides time-based and approval-based role activation to mitigate the risks of excessive, unnecessary, or misused access permissions on resources that you care about. 

## 1. License requirements

_Licensing_: P2

## 2. Admin experience

The administrator assigns roles to users, groups, service principals, or managed identities. The assignment includes the following data:

- The members or owners to assign the role.
- The scope of the assignment. The scope limits the assigned role to a particular set of resources.
- The type of the assignment
  - **Eligible** assignments require the member of the role to perform an action to use the role. Actions might include  activation, or requesting approval from designated approvers.
  - **Active** assignments don't require the member to perform any action to use the role. Members assigned as active have the privileges assigned to the role.
- The duration of the assignment, using start and end dates or permanent. For eligible assignments, the members can activate or requesting approval during the start and end dates. For active assignments, the members can use the assign role during this period of time.

For more information, check out the following articles: [Assign Azure AD roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-add-role-to-user) (and assign a role to [users](https://docs.microsoft.com/azure/active-directory/roles/manage-roles-portal) and [groups](https://docs.microsoft.com/azure/active-directory/roles/groups-pim-eligible)), [Assign Azure resource roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-add-role-to-user), and [Assign eligibility for a privileged access group](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-add-role-to-user)

## 3. User experience

The PIM role assignments give you a secure way to grant access to resources in your organization. This section describes the assignment process. It includes assign roles to members, activate assignments, approve or deny requests, extend and renew assignments. 

### 3.1 Activate

If users have been made eligible for a role, then they must activate the role assignment before using the role. To activate the role, users select specific activation duration within the maximum (configured by administrators), and the reason for the activation request.

If the role requires [approval](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-approval-workflow) to activate, a notification will appear in the upper right corner of the user's browser informing them the request is pending approval. If an approval isn't required, the member can start using the role.

For more information, check out the following articles: [Activate Azure AD roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-activate-role), [Activate my Azure resource roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-activate-your-roles), and [Activate my privileged access group roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/groups-activate-roles)

### 3.2 Extend or renew assignments

After administrators set up time-bound owner or member assignments, the first question you might ask is what happens if an assignment expires? In this new version, we provide two options for this scenario:

- **Extend** – When a role assignment nears expiration, the user can use Privileged Identity Management to request an extension for the role assignment
- **Renew** – When a role assignment has already expired, the user can use Privileged Identity Management to request a renewal for the role assignment

Both user-initiated actions require an approval from a Global Administrator or Privileged Role Administrator. Admins don't need to be in the business of managing assignment expirations. You can just wait for the extension or renewal requests to arrive for simple approval or denial.

For more information, check out the following articles: [Extend or renew Azure AD role assignments](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-renew-extend), [Extend or renew Azure resource role assignments](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-renew-extend), and [Extend or renew privileged access group assignments](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/groups-renew-extend)

### 3.3 Approver experience

Delegated approvers receive email notifications when a role request is pending their approval. Approvers can view, approve or deny these pending requests in PIM. After the request has been approved, the member can start using the role. For example, if a user or a group was assigned with Contribution role to a resource group, they'll be able to manage that particular resource group.

For more information, check out the following articles: [Approve or deny requests for Azure AD roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/azure-ad-pim-approval-workflow), [Approve or deny requests for Azure resource roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-approval-workflow), and [Approve activation requests for privileged access group](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/groups-approval-workflow)

## 4. Privileged access groups

With Privilege identity management you can [assign members or owners to a security group](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/groups-discover-groups) (type of [role-assignable groups](https://docs.microsoft.com/azure/active-directory/roles/groups-create-eligible)). The admin and user experience is identical to the [roles assignments to users, groups, service principals, or managed identities](#2-admin-experience) as described in this article. This feature allows you to add members or owners to a security group. 

When people join the group, they are assigned the role indirectly. For example, if the Application 
Administrator role has been assigned to the group, all users in that group have this role.

## 5. Role setting

An administrator can customize PIM in their Azure AD organization, including changing the experience for a user who is activating an eligible role assignment, such as security operators, or application administrator. The configuration is per role, and include the following settings:

- Activation max duration
- On activation require MFA
- Require justification on activation 
- Require approval to activate
- And select approvals

## 6. Notifications

PIM keeps you informed by sending you and other participants [email notifications](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-email-notifications). These emails might also include links to relevant tasks, such activating, approve or deny a request.

The following screenshot shows an email message sent by PIM. The email informs Patti that Alex updated a role assignment for Emily.

## 7. Audit

You can use the Privileged Identity Management (PIM) audit history to see all role assignments and activations within the past 30 days for all privileged roles. If you want to retain audit data for longer than the default retention period, you can use Azure Monitor to route it to an Azure storage account. 

For more information, check out the following articles: [View audit history for Azure AD roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-use-audit-log), [View activity and audit history for Azure resource roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/azure-pim-resource-rbac), and [Audit activity history for privileged access group assignments](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/groups-audit).

## 8. Security alerts

PIM generates alerts when there's suspicious or unsafe activity in your organization in Azure AD. When an alert is triggered, it shows up on the Privileged Identity Management dashboard. Select the alert to see a report that lists the users or roles that triggered the alert.

For more information, check out the following articles: [Configure security alerts for Azure AD roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-how-to-configure-security-alerts), and [Configure security alerts for Azure roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-configure-alerts).

[PIM alerts you](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-resource-roles-configure-alerts#alerts) when:

- Too many owners assigned to a resource
- Too many permanent owners assigned to a resource
- Duplicate role created
- **Roles are being assigned outside of Privileged Identity Management** (high risk). For example, an admin assign an active-permanent permissions to a virtual machine. PIM alerts you to review the users in the list and remove them from privileged roles assigned outside of Privilege Identity Management.

## 9. Discovery and insights

Before your organization starts using PIM, all role assignments are permanent. Users are always in their assigned roles even when they don't need their privileges. [Discovery and insights](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-security-wizard) shows you a list of privileged roles and how many users are currently in those roles. You can list out assignments for a role to learn more about the assigned users if one or more of them are unfamiliar.

## 10. Access review of Azure resource and Azure AD roles in PIM

To reduce the risk associated with stale **role assignments**, you can [create access reviews for privileged access to Azure resource and Azure AD roles](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-create-azure-ad-roles-and-resource-roles-review). The scope of the access review covers users and service principals (apps). The access review checks a **role** (selecting more than one role will create multiple access reviews), and the **assignment type**: "all active and eligible assignments", "eligible assignments only", or "active assignments only".
 
> Tip: Check also the Azure AD [access reviews](https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overview) which enables organizations to efficiently manage **group memberships**, **access to enterprise applications**. 

## 11. Elevate access to manage all Azure subscriptions and management groups

As a Global Administrator in Azure AD, you might not have access to all subscriptions and management groups in your directory. There might be times when you want to do the following actions:

- Regain access to an Azure subscription or management group when a user has lost access
- Grant another user or yourself access to an Azure subscription or management group
- See all Azure subscriptions or management groups in an organization
- Allow an automation app (such as an invoicing or auditing app) to access all Azure subscriptions or management groups

If you are a Global Administrator in Azure AD, you can [assign yourself access](https://docs.microsoft.com/azure/role-based-access-control/elevate-access-global-admin?toc=%2Fazure%2Factive-directory%2Fprivileged-identity-management%2Ftoc.json) to all Azure subscriptions and management groups in your directory. Use this capability if you don't have access to Azure subscription resources, such as virtual machines or storage accounts, and you want to use your Global Administrator privilege to gain access to those resources.
