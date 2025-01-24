


Before you decide whether you want to join a device to an AD DS domain or to Microsoft Entra ID, it’s important to understand the difference between these two concepts. Devices that join an AD DS domain must run a supported operating system version; for example, Home editions of the Windows and Windows RT operating systems don't support joining a domain. Devices that are capable of joining an AD DS domain usually access on-premises applications and services. Devices also can access some cloud resources if you integrate the domain accounts and Microsoft accounts.

Microsoft Entra join allows All Windows 11 and Windows 10 devices except Home editions, Windows Server 2019 and newer Virtual Machines running in Azure (Server core isn't supported). Devices must meet certain requirements, such as having the correct ports open and not being joined to another AD DS domain. Devices running operating systems such as Windows 10 Home, Pro, or Enterprise, Windows Server, macOS, iOS, or Android can register with Microsoft Entra ID. When you register a device with Microsoft Entra ID, it can access cloud-based resources and Azure-based resources by using SSO. From a management perspective, you can use Intune to manage and provision devices that are registered with Microsoft Entra ID. However, you can't manage these devices by using Group Policy. We'll talk more about device registration in the next unit.


#### Scenario 1: Businesses Largely in the Cloud

Microsoft Entra join (Microsoft Entra join) can benefit you if you currently operate and manage identities for your business in the cloud or are moving to the cloud soon. You can use an account that you have created in Microsoft Entra ID to sign into Windows. Through the first run experience (FRX) process, or by joining Microsoft Entra ID from the settings menu, your users can join their machines to Microsoft Entra ID. Your users can also enjoy single sign-on (SSO) access to cloud resources like Microsoft 365, either in their browsers or in Office applications.


#### Scenario 2: Educational Institutions

Educational institutions usually have two user types: faculty and students.

Faculty members are considered longer-term members of the organization. Creating on-premises accounts for them is desirable. But students are shorter-term members of the organization and their accounts can be managed in Microsoft Entra ID. This means that directory scale can be pushed to the cloud instead of being stored on-premises. It also means that students will be able to sign into Windows with their Microsoft Entra accounts and get access to Microsoft 365 resources in Office applications.

You may want to join devices to Microsoft Entra ID in these scenarios:

- **If most applications and resources that you use are in the cloud**. If you already use certain cloud services such as Microsoft 365 and you plan to move your other workloads to the cloud, you should join the client devices to Microsoft Entra ID to ensure ease of access and SSO for cloud-based services.
- **If you want to separate temporary accounts**. If you need to manage temporary accounts separately from your regular accounts, such as for contractors or seasonal workers, yet you still want to provide them with limited cloud-based services, you can create these accounts in Microsoft Entra ID and join the users' devices to Microsoft Entra ID.
- **If you want to enable users to join their own devices to the organizational environment**. If you support the Bring Your Own Device (BYOD) concept and you want to enable users to join their devices to your business environment, Microsoft Entra ID might be the right solution. This is particularly the case in situations where users are utilizing non-Microsoft devices such as iPads or Android tablets that can't join an AD DS domain, but they can enroll in Intune and Microsoft Entra ID.
- **You want to transition to cloud-based infrastructure** using Microsoft Entra ID and an MDM such Intune.
- **You have remote branch offices with limited on-premises infrastructure** and wish to provide joining capabilities to workers.

Users can join Windows devices to Microsoft Entra ID during initial Windows setup or later by opening their system settings. In both instances, users need to type in their Microsoft Entra credentials and accept the management policies.

Keep in mind that you also need to prepare Microsoft Entra ID so that it can join a device. To do this, open the Azure portal, navigate to your Microsoft Entra instance, and then open Users and groups administration pane. You can configure options for joining a device in the Device settings section.


To join a Windows device, the device registration service must be configured to enable you to register devices. In addition to having permission to joining devices in your Microsoft Entra tenant, you must have fewer devices registered than the configured maximum.

In addition, if your tenant is federated, your Identity provider MUST support WS-Fed and WS-Trust username/password endpoint. This can be version 1.3 or 2005. This protocol support is required to both join the device to Microsoft Entra ID and log on to the device with a password.

Microsoft Entra join is intended for organizations that want to be cloud-first (that is, primarily use cloud services, with a goal to reduce use of an on-premises infrastructure) or cloud-only (no on-premises infrastructure). There are no restrictions on the size or type of organizations that can deploy Microsoft Entra join. Microsoft Entra join works well even in a hybrid environment, enabling access to both cloud and on-premises apps and resources.

Implementing Microsoft Entra joined devices provides you with the following benefits:

- Single-Sign-On (SSO) to your Azure managed SaaS apps and services. Your users don’t see additional authentication prompts when accessing work resources. The SSO feature remains accessible even when disconnected from the domain network.
- Enterprise compliant roaming of user settings across joined devices. Users don’t need to connect a Microsoft account (for example, Hotmail) to see settings across devices.
- Windows Hello support for secure and convenient access to work resources.
- Restriction of access to apps from only devices that meet compliance policy.
- Seamless access to on-premises resources when the device has line of sight to the on-premises domain controller.

For organizations that have on-premises Windows Server Active Directory infrastructure, using Microsoft Entra ID offers:

- You want to transition to cloud-based infrastructure using Microsoft Entra ID and mobile device management (MDM) like Intune.
- Scenarios where you can’t use an on-premises domain join. For example, if you need to get mobile devices such as tablets and phones under control.
- Your users primarily need to access Microsoft 365 or other SaaS apps integrated with Microsoft Entra ID.
- You want to manage a group of users in Microsoft Entra ID instead of in Active Directory. This can apply, for example, to seasonal workers, contractors, or students.
- You want to provide joining capabilities to workers in remote branch offices with limited on-premises infrastructure.

# Join devices to Microsoft Entra ID

Completed100 XP

- 2 minutes

Joining a device to Microsoft Entra ID is not a complicated procedure. You can do it right after the Windows OS installation, or you can do it later, at any time. To join a Windows device to Microsoft Entra ID at the end of Windows setup process, follow these steps:

1. When you turn on your new device and start the setup process, you should see the Getting Ready message. Follow the prompts to set up your device.
    
2. Start by customizing your region and language. Then accept the Microsoft Software License Terms.
    
    ![Screenshot of the Customize for your region screen.](https://learn.microsoft.com/en-us/training/wwl-azure/administer-device-authentication/media/customize-region-a7af67b2.png)
    
3. Select the network you want to use for connecting to the internet.
    
4. Select **This device belongs to my organization**.
    
    ![Screenshot showing Who owns this PC? screen.](https://learn.microsoft.com/en-us/training/wwl-azure/administer-device-authentication/media/personal-computer-owner-02d1488b.png)
    
5. Enter the credentials that were provided to you by your organization, and then select **Sign in**.
    
    ![Screenshot of the Sign in screen.](https://learn.microsoft.com/en-us/training/wwl-azure/administer-device-authentication/media/work-account-sign-419af822.png)
    
6. Your device locates a matching tenant in Microsoft Entra ID. If you’re in a federated domain, you’re redirected to your on-premises Secure Token Service (STS) server, for example, Active Directory Federation Services (AD FS).
    
7. If you’re a user in a non-federated domain, enter your credentials directly on the Microsoft Entra ID-hosted page.
    
8. You’re prompted for a multifactor authentication challenge.
    
9. Microsoft Entra ID checks whether an enrollment in mobile device management is required.
    
10. Windows registers the device in the organization’s directory in Microsoft Entra ID and enrolls it in mobile device management, if applicable.
    
11. If you are:
    
    - A managed user, Windows takes you to the desktop through the automatic sign-in process.
    - A federated user, you’re directed to the Windows sign-in screen to enter your credentials.

Group Policy or Microsoft Configuration Manager applications mostly manage devices that are capable of joining AD DS. When you join a device to Microsoft Entra ID, Group Policy isn't available except when you use with Microsoft Entra Domain Services. However, even with Microsoft Entra Domain Services, Group Policy can't manage devices such as smartphones and tablets.

Microsoft Entra ID doesn't provide a built-in management mechanism for devices that don't support Group Policy. Additionally, Microsoft Entra Domain Services isn't enabled by default, you must manually enable and configure this service.

If you want to manage devices that join Microsoft Entra ID, you can configure integration between Azure and a mobile device management mechanism such as Intune. If you configure Intune as an application in Azure, each device that joins Microsoft Entra ID can be configured to enroll in Intune automatically. For this to work, you need to have an active Intune subscription that’s associated with the same Microsoft Entra tenant where you configured the integration of these services. Additionally, a user who joins a device to Microsoft Entra ID needs to have an assigned Intune license.

After the device enrolls in Intune, you can configure Intune security and configuration policies that will apply to the user or to the device. It’s important to understand that management through Intune doesn't follow the same logic as management with Group Policy, nor does it have as many available options. Intune management options mostly focus on security and the apps that are on managed devices.