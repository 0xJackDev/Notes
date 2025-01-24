

Similar to locally deployed AD DS, you manage Microsoft Entra objects and settings, but by using a different set of tools. When using Microsoft Entra ID, you'll need to create users, groups, and devices. Also, you can use role-based access control (RBAC) in Azure to configure and delegate permissions. Unlike AD DS, you can manage multiple Microsoft Entra tenants by using an account from a single tenant. In this lesson, you'll learn how to manage Microsoft Entra ID.

After this module, you should be able to:

- Describe RBAC and user roles in Microsoft Entra ID.
- Create and manage users in Microsoft Entra ID.
- Create and manage groups in Microsoft Entra ID.
- Use Windows PowerShell cmdlets to manage Microsoft Entra ID.
- Describe how you can synchronize objects from AD DS to Microsoft Entra ID.

Microsoft Entra ID has a SaaS operational model and lacks support for computer objects and management capabilities via Group Policy settings. Therefore, the delegation model within Microsoft Entra ID is considerably simpler than the same model in AD DS. There are several built-in roles in all three tiers, including Global Administrator, Billing Administrator, Service Administrator, User Administrator, and Password Administrator. Each role provides different levels of directory-wide permissions to its objects. By default, the Account Administrator of the subscription hosting the Microsoft Entra instance is assigned as the Global Administrator, with full permissions to all objects in their directory instance. The Service Administrator, however, has more limited permissions and isn't the same as the Global Administrator by default.

In Microsoft Entra ID, using the delegation model, you can delegate permissions to applications, allowing them to act on behalf of users and groups. The depth and breadth of these delegation capabilities vary based on the Microsoft Entra edition. With Microsoft Entra ID Free, you can assign applications to both users and groups. The Microsoft Entra ID P1 edition enhances this by offering more advanced assignment capabilities, such as dynamic group membership based on user attributes. The Premium P2 edition builds upon this by introducing features like self-service group management, where users can create and manage their own groups, and Privileged Identity Management (PIM), which is part of the suite of Identity Governance tools, allowing users to elevate their privileges temporarily.

Microsoft Entra users can access Microsoft Entra applications by using the web-based portal, referred to as My Apps, at _[https://myapps.microsoft.com](https://myapps.microsoft.com/)_. This portal automatically presents to the users all applications for which they have permissions. Another benefit of using this approach is the support for SSO. When starting an individual application from its interface, authentication happens automatically once users sign in to the portal.

### Azure delegation model and role-based access control

The delegation model applies to the graphical interface that is available in the Azure portal. The Azure portal offers a much more flexible and precise way of restricting management of Azure resources by implementing RBAC. This mechanism relies on three built-in roles: owner, contributor, and reader. Each of these roles performs a specific set of actions on Azure resources that are exposed via the Azure portal—resources such as websites or SQL databases. You can grant the intended access by associating a Microsoft Entra object such as a user, group, or service principal with a role and a resource that appears in the Azure portal.

Microsoft Entra ID doesn't include the OU class, which means that you can't arrange its objects in a hierarchy of custom containers, which frequently are used in on-premises AD DS deployments. This isn’t a significant shortcoming, because OUs in AD DS are used primarily for Group Policy scoping and delegation. Instead, you can accomplish equivalent arrangements by organizing objects based on their attribute values or group membership.

### User roles in Microsoft Entra ID

You can use three types of accounts with Microsoft Entra ID:

- An organizational account that the tenant administrator or a co-administrator creates within the default Azure directory or any custom Azure directory—for example, user@domain1.onmicrosoft.com.
- An account that references an organizational account you create in other Microsoft Entra instances—for example, user@domain2.onmicrosoft.com.
- An account that references a Microsoft account—for example, user@outlook.com.

You use the tenant administrator account to sign up for a new trial or paid subscription. This account can be a Microsoft account or an existing organizational account. To avoid mixing authentication methods, we recommend that you use organizational accounts to manage your Microsoft Entra tenant.

You can only manage Microsoft Entra ID if you're a Global Administrator of the Microsoft Entra instance. You can only sign in to an Azure portal if you’re the tenant administrator or if the tenant administrator has configured an organizational account to be a co-administrator.

 Note

Tenant administrators and co-administrators can manage Microsoft Entra ID by using the Azure portal because by default these accounts automatically are granted the Global Administrator role in the Active Directory instance that is associated with the subscription.

Within Microsoft Entra ID, you can configure users with the following roles:

- **Global Administrator**. This role has access to all administrative features and settings. When you sign up for the Azure subscription, you become a Global Administrator. Only this role can assign administrative roles to other accounts.
    
- **Limited administrator**. When you select the Limited administrator role for the user, you can then select one or more of the following administrative roles (the list can vary based on applications that are using your Microsoft Entra ID):
    
    - **Password Administrator** can reset passwords for users and manage service requests.
    - **Service Administrator** can manage service requests.
    - **Billing Administrator** can manage billing information.
    - **Exchange Administrator** can manage Exchange Online settings.
    - **Skype for Business Administrator** can manage Skype for Business Online settings.
    - **User Administrator** can manage user accounts and groups.
    - **SharePoint Administrator** can manage SharePoint Online settings.
    - **Compliance administrator** can manage compliance settings.
    - **Security reader** can read security settings.
    - **Security Administrator** can manage security settings.
    - **Privileged role Administrator** can manage privileged roles.
    - **Intune Administrator** can manage Intune settings.
    - **Guest inviter** can invite guest users to the organization.
    - **Conditional Access Administrator** can manage conditional access settings.
- **User**. This is a default role that doesn't provide any administrative rights.
    

These roles are applicable to management tools such as the Microsoft 365 and Intune portals, or the Azure AD module for Windows PowerShell cmdlets. When you’re using Privileged Identity Management, you can also configure the Security reader and Security administrator roles.




# Create and manage users in Microsoft Entra ID

Completed100 XP

- 2 minutes

You can manage Microsoft Entra users, groups, and devices by using the Azure portal, the Microsoft Azure Active Directory module for Windows PowerShell, or Microsoft 365. You can add users to a directory, and also add users to groups.

You can create two types of user accounts on the Azure portal:

- **Member users:** Are accounts that your Microsoft Entra tenant manages. After creating a user, you can configure user properties. Member users are the most commonly created user type.
- **Guest users:** Are accounts that your Microsoft Entra tenant doesn’t manage, but you want to assign permissions to the users. A guest user account is a member user from another Microsoft Entra tenant or a Microsoft account. Although administrators can create these accounts, these accounts are often created automatically when users share content with external users. For example, if you share a OneDrive file with a user, then a Guest user account is created.

There are essentially two ways to create and manage your users:

- **As cloud identities by using only Microsoft Entra ID** This option is the quickest and most straightforward method.
- **As directory-synchronized identities by using an on-premises directory service to synchronize with Microsoft Entra ID:** This method has the added complexity of installing and configuring synchronization software to ensure that directory objects synchronize successfully with Microsoft Entra ID.

The Azure portal provides a simple web interface for creating and managing users, groups, and devices.

#### Create and manage users with the Azure portal

Using the Azure portal is the simplest method for creating single or small numbers of user accounts.

To create a single user, perform the following steps:

1. In the Azure portal, on the left pane, select **Microsoft Entra ID**.
    
2. Select **Users and groups**, and then select **All users**.
    
3. Select **+ New user**.
    
4. Enter the following user information:
    
    - Name
    - User name: < unique name >
    - Profile - First Name/Last Name/Display Name: (choose appropriate values)
    - Properties: choose source of authority (default is Microsoft Entra ID)
    - Groups: Select groups to which you want the new user to belong
    - Directory role: User, Global administrator, or Limited administrator
5. Select **Create** to finalize user creation. After the user is created, a temporary password appears.


Just as groups in Active Directory Domain Services (AD DS) simplify permissions management, Microsoft Entra groups streamline access management. When you enable directory synchronization, your on-premises AD DS groups can be synchronized to Microsoft Entra ID. While the group membership remains consistent between AD DS and Microsoft Entra ID, the individual members are mapped from on-premises user accounts to their corresponding Microsoft Entra accounts. If directory synchronization isn't in place, group management is exclusively cloud-based.

In Microsoft Entra ID, you can establish two primary types of groups:

- **Security**. A security group is designed to manage resource access. By assigning permissions to a security group, you can control access based on group membership. For instance, if you create a security group named **Sales**, you can grant this group access to a specific file share. Managing the **Sales** group membership then indirectly manages access to that file share. Contrary to some misconceptions, Microsoft Entra security groups aren't mail-enabled.
    
- **Microsoft 365**. A Microsoft 365 group facilitates access management for Microsoft 365 services, including Microsoft Teams, SharePoint, and Outlook. For example, if you establish a Microsoft 365 group named **Sales**, you can delegate permissions for this group to access a SharePoint site. Managing the group's membership then determines access to that site. By design, Microsoft 365 groups are mail-enabled, serving dual purposes as collaboration groups and email distribution lists.
    

To create a group in Azure, navigate to **Microsoft Entra ID** > **Groups** > **New group** on the Azure portal. Here, you can specify the group type, name, and description. You'll also choose whether it's a security group or a Microsoft 365 group. Remember, only Microsoft 365 groups are inherently mail-enabled.

#### Assign Membership

Membership for a cloud-based group can be **assigned** or **dynamic**. When you create a group with assigned membership, you need to add and remove group members manually. When you create a group with dynamic membership, members are based on a query of Microsoft Entra objects. For example, dynamic membership can be based on a user’s department. You can create a membership rule based on a single attribute or an advanced membership rule where you can create complex queries based on multiple attributes.

When you create a group with dynamic membership, you need to select whether it’s for users or devices. Many Microsoft 365 features can use user-based groups. Intune uses device-based groups.

Groups from on-premises AD DS with dynamic membership don’t synchronize with Microsoft Entra ID.

You can also manage users, groups, and devices by using the Microsoft Graph PowerShell SDK. This approach uses the unified Microsoft Graph API, providing a comprehensive and efficient way to automate management tasks across Microsoft 365 services. PowerShell 7 and later is the recommended PowerShell version for use with the Microsoft Graph PowerShell SDK on all platforms. There are no more prerequisites to use the SDK with PowerShell 7 or later. For more information, see [Install the Microsoft Graph PowerShell SDK](https://learn.microsoft.com/en-us/powershell/microsoftgraph/installation?view=graph-powershell-1.0)

Before you begin, ensure you have the following requirement:

- **Operating system** A Windows 10 or later, or a supported version of Windows Server.
- **PowerShell**. You must have PowerShell 5.1 or newer, or PowerShell Core.
- **Microsoft Graph PowerShell SDK**. The Microsoft Graph PowerShell SDK installed. If you haven't installed it yet, you can do so by running the following command in PowerShell:

PowerShellCopy

```
Install-Module -Name Microsoft.Graph -scope CurrentUser
```

### Connecting to Microsoft Entra with Microsoft Graph PowerShell SDK

To connect to Microsoft Entra, you can use the `Connect-MgGraph` cmdlet. This cmdlet prompts you to sign in to your Microsoft Entra account and then creates a connection to the Microsoft Graph service. You can then use the connection to run cmdlets to manage users, groups, and devices.

PowerShellCopy

```
Connect-MgGraph -Scopes "User.Read.All", "Group.ReadWrite.All", "Device.ReadWrite.All"
```

Adjust the scopes according to the permissions required for your specific tasks.

### Create users by using bulk import

You can import a .csv file containing account information to create multiple users in bulk, such as exporting from an existing on-premises directory, or use Microsoft Graph PowerShell SDK scripting to generate multiple accounts. To use bulk import, you first must assemble your user information, which might include the following table:

Expand table

|UserName|FirstName|LastName|DisplayName|JobTitle|Department|
|---|---|---|---|---|---|
|AnneW@adatum.com|Anne|Wallace|Anne Wallace|President|Management|
|FabriceC@adatum.com|Fabrice|Canel|Fabrice Canel|Attorney|Legal|
|GarretV@adatum.com|Garret|Vargas|Garret Vargas|Operations|Operations|

Use the following script to read the .csv file and create the user accounts in Microsoft Entra:

PowerShellCopy

```
$users = Import-Csv -Path "C:\path\to\your\Users.csv"

foreach ($user in $users) {
    New-MgUser -UserPrincipalName $user.UserName `
               -GivenName $user.FirstName `
               -Surname $user.LastName `
               -DisplayName $user.DisplayName `
               -JobTitle $user.JobTitle `
               -Department $user.Department `
               -AccountEnabled $true `
               -MailNickname $user.FirstName `
               -UsageLocation "US" `
               -PasswordProfile @{ForceChangePasswordNextSignIn = $true; Password = "Password"}
}
```

This script reads the .csv file and creates a new user for each row in the file. The `New-MgUser` cmdlet creates a new user in Microsoft Entra with the specified properties.

By using the Microsoft Graph PowerShell SDK, you can efficiently manage Microsoft Entra objects with the flexibility and power of Microsoft Graph. This guide has introduced you to connecting to Microsoft Graph and creating users in bulk. Explore further to discover the full potential of automating your Microsoft 365 administration tasks with Microsoft Graph PowerShell.

# Synchronize objects from AD DS to Microsoft Entra ID

Completed100 XP

- 5 minutes

Numerous deployment scenarios for Microsoft Entra don’t involve an on-premises AD DS environment. However, for many organizations that have some services on their networks and some services in the cloud, synchronization and integration between Microsoft Entra ID and on-premises AD DS is the way to deliver the best user experience. Directory synchronization enables user, group, and contact synchronization between on-premises Active Directory and Microsoft Entra ID. In its simplest form, you install a directory synchronization component on a server in your on-premises domain. All your user accounts, groups, and contacts from Active Directory then replicate to Microsoft Entra ID. Those accounts can then sign in and access Azure services.

With Microsoft Entra ID Free or Basic, the synchronization flow is in one direction, from local AD DS to Microsoft Entra ID. However, with Microsoft Entra ID P1 or P2, you can replicate some attributes from Microsoft Entra ID to Active Directory DS. For example, you can configure Microsoft Entra ID to write passwords back to an on-premises AD DS.

#### Microsoft Entra Connect

Microsoft provides Microsoft Entra Connect to perform directory synchronization between Microsoft Entra ID and AD DS. By default, Microsoft Entra Connect synchronizes all users and groups. If you don’t want to synchronize your entire on-premises AD DS, directory synchronization for Microsoft Entra ID supports limited filtering and customization of attribute flow based on the following values:

- OU
- Domain
- User attributes
- Applications

When directory synchronization is enabled, you have the following authentication options:

- **Separate cloud password**. When you synchronize a user identity and not the password, the cloud-based user account will have a separate unique password. This can be confusing for users.
- **Synchronized password**. If you enable password synchronization, the AD DS user password syncs with the identity in Microsoft Entra ID. This allows users to authenticate by using the same credentials, but it doesn’t provide seamless SSO, because users still receive prompts to authenticate cloud services.
- **Pass-through authentication**. When you enable pass-through authentication, Microsoft Entra ID uses the cloud identity to verify that the user is valid, and then passes the authentication request to Microsoft Entra Connect. This option provides true SSO because users don’t receive multiple prompts to authenticate cloud services.
- **Federated identities**. If you configure federated identities, the authentication process works similarly to pass-through authentication, but AD FS performs authentication on-premises instead of Microsoft Entra Connect. This authentication method provides claims-based authentication that multiple cloud-based apps can use.

When you install Microsoft Entra Connect, you need to sign in as a local Administrator of the computer on which you're performing installation. Additionally, you'll receive prompts for credentials to the local AD DS and Microsoft Entra ID. The local AD DS account must be a member of the enterprise administrators group. The Microsoft Entra account must be a global administrator. If you’re using AD FS or a separate SQL Server instance, you'll also receive prompts for credentials with management permissions for those resources.

The computer that is running Microsoft Entra Connect needs to communicate with Microsoft Entra ID. If the computer needs to use a proxy server for internet access, then more configuration is necessary. No inbound connectivity from the internet is necessary because Microsoft Entra Connect initiates all communication.

Microsoft Entra Connect must be on a domain member. Installing Microsoft Entra Connect on a domain controller is supported, but this typically occurs only in smaller organizations with limited licensing.

When you install Microsoft Entra Connect, you can use express settings or custom settings. Most organizations that synchronize a single AD DS forest with a Microsoft Entra tenant use the express settings option. When you choose express settings, the following options are selected:

- SQL Server Express is installed and configured.
- All identities in the forest are synchronized.
- All attributes are synchronized.
- Password synchronization is enabled.
- An initial synchronization is performed immediately after install.
- Automatic upgrade is enabled.

You can enable other options during installation when you select custom settings, such as:

- Pass-through authentication.
    
- Federation with AD FS.
    
- Select an attribute for matching existing cloud-based users.
    
- Filtering based on OUs or attributes.
    
- Exchange hybrid.
    
- Password, group, or device writeback.
    
- After deploying Microsoft Entra Connect, the following occurs:
    
    - New user, group, and contact objects in on-premises Active Directory are added to Microsoft Entra ID; however, no licenses for cloud services, such as Microsoft 365, are automatically assigned to these objects.
    - Attributes of existing user, group, or contact objects that are modified in on-premises Active Directory are modified in Microsoft Entra ID; however, not all on-premises Active Directory attributes synchronize with Microsoft Entra ID.
    - Existing user, group, and contact objects that are deleted from on-premises Active Directory are deleted from Microsoft Entra ID.

Existing user objects that are disabled on-premises are disabled in Azure; however, licenses aren’t automatically unassigned.


