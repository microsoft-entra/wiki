# Azure AD Connect cloud sync

[Azure AD Connect cloud sync](https://docs.microsoft.com/azure/active-directory/cloud-sync/what-is-cloud-sync?toc=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fazure%2Factive-directory%2Fcloud-sync%2Ftoc.json&bc=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fazure%2Fbread%2Ftoc.json) (in short 'cloud sync') is a new offering designed to meet and accomplish organizations hybrid identity goals for **synchronization of users, groups, and contacts to Azure AD**. It replaces the [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-azure-ad-connect-v2). For more information, check out the [Comparison between Azure AD Connect and cloud sync](https://docs.microsoft.com/azure/active-directory/cloud-sync/what-is-cloud-sync?toc=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fazure%2Factive-directory%2Fcloud-sync%2Ftoc.json&bc=https%3A%2F%2Fdocs.microsoft.com%2Fen-us%2Fazure%2Fbread%2Ftoc.json#comparison-between-azure-ad-connect-and-cloud-sync) article.


## 1. Azure AD Connect cloud sync key features

Azure AD Connect cloud sync provides the following benefits:

- The sync accomplishes by using the **Azure AD cloud provisioning agent**. It's a light-weight provisioning agent. The agents act as a bridge from AD to Azure AD, with all the sync configuration managed in the cloud. 
  - It's the [same agent](https://docs.microsoft.com/azure/active-directory/cloud-sync/concept-how-it-works#overview-of-components) as Workday inbound and built on the same server-side technology as app proxy and Pass Through Authentication. 
  - It requires an **outbound** connection only and agents are auto-updated.
- Changes are provisioned [every 2 mins](https://docs.microsoft.com/azure/active-directory/cloud-sync/concept-how-it-works#overview-of-components).
- The provisioning configuration is stored in Azure AD and managed as part of the service (and not in the on premises).
- Multiple provisioning agents can be used to simplify high availability deployments, particularly critical for organizations relying upon password hash synchronization from AD to Azure AD.
- It can be used alongside Azure AD Connect. For cases like merger & acquisition (where the acquired company's AD forests are isolated from the parent company's AD forests).
- The Azure AD Connect cloud provisioning agent uses [SCIM with Azure AD](https://docs.microsoft.com/azure/active-directory/cloud-sync/concept-how-it-works) to provision and deprovision users and groups.
- Supports password hash synchronization

## 2. Attribute mapping

You can [map attributes](https://docs.microsoft.com/azure/active-directory/cloud-sync/how-to-attribute-mapping) between your on-premises user or group objects and the objects in Azure AD. With attribute mapping, you control how attributes are populated in Azure AD. Azure AD supports four mapping types: 

- **Direct** - The target attribute is populated with the value of an attribute of the linked object in Active Directory.
- **Constant** - The target attribute is populated with a specific string that you specify
- **Expression** - The target attribute is populated based on the result of a script-like expression. For more information, check out the following articles: [Expression Builder](https://docs.microsoft.com/azure/active-directory/cloud-sync/how-to-expression-builder) and [Writing expressions for attribute mappings](https://docs.microsoft.com/azure/active-directory/cloud-sync/reference-expressions).

### 2.1 Map the user type with cloud sync

By default, the [UserType attribute](https://docs.microsoft.com/azure/active-directory/external-identities/user-properties) isn't enabled for synchronization because there's no corresponding UserType attribute in on-premises Active Directory. You must [manually add this mapping](https://docs.microsoft.com/azure/active-directory/cloud-sync/how-to-map-usertype) for synchronization. Azure AD only accepts two values for the UserType attribute: Member and Guest. 

## 3. Accidental delete prevention

The [accidental delete](https://docs.microsoft.com/azure/active-directory/cloud-sync/how-to-accidental-deletes) feature is designed to protect you from accidental configuration changes and changes to your on-premises directory that would affect many users and groups

## 4. Automatic upgrade

Make sure your Azure AD Connect cloud provisioning agent installation is always up to date is easy with the automatic upgrade feature. Check out the [Azure AD Connect cloud provisioning agent: Automatic upgrade](https://docs.microsoft.com/azure/active-directory/cloud-sync/how-to-automatic-upgrade) article to verify your version.

## 5. Migrate to Could sync

The cloud sync can be used alongside Azure AD Connect. It allows you to gradually migrate the Azure AD Connect to the Azure AD cloud sync. Check out the [Pilot cloud sync for an existing synced AD forest](https://docs.microsoft.com/azure/active-directory/cloud-sync/tutorial-pilot-aadc-aadccp) tutorial. 