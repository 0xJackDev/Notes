# Introduction

Completed100 XP

- 3 minutes

As organizations continue to embrace digital transformation, the need for efficient and secure device management solutions has become increasingly important. With the advent of Windows Autopilot and co-management through Configuration Manager and Microsoft Intune, organizations can now streamline device provisioning and management in the modern era. This introductory module will guide you through the key concepts and considerations for transitioning to modern device management using Windows Autopilot and co-management.

In this module, you'll learn Windows Autopilot, co-management, and the benefits of combining these technologies. You'll learn about different usage scenarios for Microsoft Entra join, workloads that can be transitioned to Intune, and the prerequisites for co-management. Additionally, we'll discuss the considerations and planning for a successful transition to modern management using both existing and new technologies.

By the end of this module, you'll have a solid understanding of Windows Autopilot, co-management, and the necessary steps to transition to modern device management. You'll also be able to plan a successful migration or provisioning strategy for your organization using these powerful tools.

### Objectives

After completing this module, you'll be able to:

- Identify usage scenarios for Microsoft Entra join.
- Identify workloads that you can transition to Intune.
- Identify prerequisites for co-management.
- Identify considerations for transitioning to modern management.
- Plan a transition to modern management using existing technologies.
- Plan a transition to modern management using Microsoft Intune.



Moving to modern management can sometimes be a challenging task considering the complexity of planning and switching from existing IT systems, organizational structures, and processes. Most organizations are still using some combination of on-premises Windows Server Active Directory (AD) and Configuration Manager to manage their Windows devices. To help IT professionals simplify the transition to modern management, Microsoft designed a new feature called Co-management.

If you have an on-premises Active Directory environment and you want to co-manage your domain-joined devices, you can accomplish this by configuring Microsoft Entra hybrid joined devices. By bringing your devices to Microsoft Entra ID, you maximize your users' productivity through single sign-on (SSO) across your cloud and on-premises resources. At the same time, you can secure access to your cloud and on-premises resources with conditional access, which is a capability of Microsoft Entra ID. With conditional access, you can implement automated access control decisions for accessing, for example, SharePoint Online or Exchange Online, that's based on conditions.

Intune gives you a way to configure settings that achieve your administrative intent without exposing every possible setting. In contrast, Group Policy exposes fine-grained settings that you control individually. With Intune, you can apply broader privacy, security, and application management settings through lighter and more efficient tools. Intune also allows you to target internet-connected devices to manage policies without using Group Policy that requires on-premises domain-joined devices. This makes MDM the best choice for devices that are constantly on the go.

When co-management is configured and ready to use, you should create one or more pilot groups of users and devices. Use these groups as part of a phased rollout of co-management. You can start with small test groups, and then add more users and devices as you roll out co-management in your environment. A good strategy is to start your pilot with users and devices from the IT department. When you're confident that it works, you can easily expand your pilot to the rest of your environment.


|--|MDT|Configuration Manager|Windows Autopilot|
|---|---|---|---|
|Require the creation of golden images|Yes|Yes|No|
|Ability to reset existing OS|No|No|Yes|
|Ability to perform a bare metal builds|Yes|Yes|No|
|Can be used with any preinstalled operating system|Yes|Yes|Windows 10/11 only|
|Installation of applications during OS deployment/provisioning|Yes|Yes|Yes|
|Deployment of applications post-builds|No|Yes|Yes|
|Migration of user data|Yes - USMT|Yes - USMT|Yes - OneDrive/ESR|
|Perform an in-place upgrade|Yes|Yes|Yes (in combination with Configuration Manager)|

After you've considered these requirements, there are two paths for transition:

- Migration of existing technologies and utilizing the benefits that each setup can offer.
- An adoption of modern technologies from the outset.

The remaining units in this module examine some of the key aspects around these paths.

### Image with Modern Methods

While modern methods of management are preferred due to their ease of configuration and administration, there are situations where traditional methods using imaging become necessary. These scenarios often arise in day-to-day operations, and some common examples include:

- When a device encounters a Blue Screen of Death (BSOD) and fails to boot into Windows, requiring a fresh installation from scratch.
- Deploying a series of complex applications and their dependencies to a device that is already co-managed.
- Dealing with hardware failures on a device that necessitate network connectivity for application installation or joining a corporate Active Directory domain.

These scenarios commonly occur when handling tasks such as replacing client storage drives, conducting bare-metal deployments, or dealing with devices that can't be upgraded to the desired operating system.

---

## Next unit: Evaluate upgrades and migrations in modern transitioning



Device migration is like deploying a new device. The deployment to the target device, whether it be the same or a different device, is typically the same process as a new device. You can use a traditional process, such as reimaging the device, or if the target device has Windows 11, you can use modern methods, such as Autopilot.

The key difference is consideration for the end user's data and configuration. The process must include a way to safely and securely ensure that user data and settings aren't lost during the process.

Scenarios for migrating users can include:

- The user's device is being replaced.
- The user's existing device is being upgraded from an older OS to Windows 11 and an in-place upgrade isn't possible (such as an unsupported upgrade path).
- A clean installation is needed. You may want to do this if the current state of the PC is undesirable. For example, the PC has performance or stability issues unrelated to hardware or the device hasn't been ideally maintained (it has legacy or unapproved apps installed, non-standard configuration, etc.)

Depending on your environment, you can use two migration scenarios: side-by-side migration or wipe-and-load migration, which is also referred to as a refresh migration. In a refresh migration scenario, the source computer and the destination computer are the same, whereas in a side-by-side migration scenario, the source computer and the destination computer are different. Both migration scenarios require a clean installation of Windows 11. When you migrate configurations from an older version of the Windows operating system, you're moving files and settings to a clean installation of the Windows operating system.

Careful consideration should be given when choosing to migrate instead of upgrade. Whenever an in-place migration is performed, there can be a risk of loss of data if either IT or the user didn't properly identify data that needed to be migrated. If something goes wrong during the deployment, a migration can't be rolled back.

Expand table

|**In-place upgrade**|**Migration**|
|---|---|
|Preserves the environment|Provides a standardized environment|
|Doesn't need to reinstall apps or transfer data|You can control what migrates|
|Upgrade can be rolled back if needed|Cleans up the environment|
|Only certain upgrade paths are possible|You must reinstall the apps|
|You must use the default Windows image|You can use a custom Windows image|

The process of preparing the destination computer isn't unlike deploying a new computer or refreshing an existing one. In the case of side-by-side migrations, if the new device has Windows 11, you can use modern methods like Autopilot to configure the device. If performing an in-place migration, you can use Autopilot for existing devices or you can use traditional methods, as well.

### In-place upgrades

Modern desktop deployment with Windows Autopilot helps you easily deploy the latest version of Windows to your existing devices. You can adapt this method for an existing legacy device (such as Windows 7/8.1) to both transform a traditional domain joined endpoint into a Microsoft Entra ID managed device and perform a rebuild, all within the same piece of automation. Alternatively, you must build devices from fresh using Autopilot from a vanilla Windows 11 PC.

![Screenshot of Task Sequence Editor showing Autopilot for existing devices options.](https://learn.microsoft.com/en-us/training/wwl/plan-transition-modern-endpoint-management/media/autopilot-for-existing-devices-task-sequence-editor-21352361.png)

As with many of the options that exist in a deployment strategy, transforming a device is only relevant if this fits into your overall planning approach. You may want to begin your journey with newly provisioned devices and migrate over time.

With tools such as Microsoft Intune and Autopilot, device deployment and the deployment scenarios are beginning to change. Co-management offers that bridge to spread workloads between Intune and Configuration Manager. This means that co-management can offer a path to modern management (with a workflow moved fully to Intune) or it can be part of the journey in helping an enterprise get to modern management by allowing it to trial the workload in Intune while running most production clients from Configuration Manager.

 Tip


# Migrate data when modern transitioning

Completed100 XP

- 11 minutes

When moving a user to a new device or performing an in-place migration, it's important to think about which user and app settings should be kept and how to make sure this information is saved.

### Synchronize the user state

Starting with Windows 10, Microsoft Entra users gain the ability to securely synchronize their user settings and application settings data to the cloud. Enterprise State Roaming (ESR) provides users with a unified experience across their Windows devices and reduces the time needed for configuring a new device. Enterprise State Roaming operates similar to the standard consumer settings sync that was first introduced in Windows 8.

Enterprise State Roaming also offers:

- **Separation of corporate and consumer data**. Organizations possess complete control over their data, guaranteeing that there's no commingling of corporate data within a consumer cloud account or consumer data within an enterprise cloud account.
- **Enhanced security**. Data is automatically encrypted before leaving the user’s Windows device by using Azure Rights Management (Azure RMS), and data stays encrypted at rest in the cloud. All content stays encrypted at rest in the cloud, except for the namespaces, like settings names and Windows app names.
- **Better management and monitoring**. Provides control and visibility over who syncs settings in your organization and on which devices through the Microsoft Entra admin center integration.

ESR (Enterprise State Roaming) facilitates the synchronization of settings across Microsoft Entra joined devices. When ESR is enabled in an organization, users simply need to sign in to a new device, and the device will automatically retain all the supported settings. These include Microsoft Edge browser settings, personalized configurations, passwords, language preferences, mouse settings, and even certain UWP Apps (if supported by the developer).

As a general guideline, it's advisable to migrate all the settings and data that users require, while avoiding the migration of unnecessary and outdated data that only takes up storage space. Additionally, it's essential to consider the effort required to migrate specific data versus the time saved.

ESR (Enterprise State Roaming) doesn't synchronize settings for desktop applications. The impact of this limitation depends on various factors. Although many applications store data in the AppData folder, often this data is generated by the app as part of its regular operations, and it may not be critical or unique data that users would consider lost if it weren't migrated.

Sometimes the user data is easier to create. For example, perhaps the user that launches a fresh installed app might have to set up something simple such as their name in the app.

It's important not to overlook simple configurations that can have a significant impact. Even if a configuration step seems straightforward, such as setting a folder location within an application, it may not be wise to assume that users will correctly configure it on their own. Relying on users to perform multiple post-migration configurations, even if they're simple, can potentially lead to issues and complications. Therefore, it's recommended to consider the potential challenges and problems that may arise from relying solely on user-initiated configurations after migration.

### Migrate the user state

When synchronization solutions aren't enough and there's a need to migrate files or settings from one device to another in Windows environments, the User State Migration Tool (USMT) is typically used. USMT isn't so much a user state synchronization tool as a means to migrate the user state during upgrades and migrations. User state migration has two phases:

1. **Capture settings**. You begin by capturing settings and data from the source computer. You store these settings in a migration store, which is often on a shared network folder, although it could also be on local storage.
2. **Restore captured settings**. After capturing the settings and data from the source computer, you must restore them on the destination computer. You can perform the second phase only after you install an operating system on the destination computer, and it can occur separately or during the operating-system installation.

Usually, all the settings and data that were captured on the source computer are later restored, but this isn't necessarily the case. You could capture some settings or data and decide later not to restore them. However, you should be aware that you can’t restore data that you didn't first capture, because it doesn't exist in the migration store.

### User state migration in the replace and refresh computer scenario

User state migration can occur in different deployment stages, depending on whether you use a wipe-and-load (refresh) or side-by-side (replace) deployment scenario.

- **In the replace scenario, the source and destination computers are different**. When deploying Windows on new computers, you can capture the user state from source computers before or after you deploy Windows on destination computers. After Windows deploys on destination computers, you can restore the user states on these computers.
- **In the refresh scenario, the source and destination computers are the same**. When upgrading to the Windows 10 or Windows 11 operating system on computers that have existing operating systems, you can capture the user state, store it in temporary storage, perform a clean Windows installation, and then restore the user state on the upgraded computers.

When you deploy Windows on a computer that has an existing, supported Windows operating system, Windows creates a Windows.old folder. You can migrate user settings from that folder. Windows enables nondestructive deployment because a Windows installation doesn't wipe out the target partition. The previous Windows installation folder, the Program Files folder, and the Users folder are moved to the Windows.old folder, whereas user data in the root folder remains unchanged. You can capture user state either online, while an older version of Windows is running, or offline, from the Windows.old folder.

### Known Folder Move to facilitate a modern file management solution

OneDrive allows users to seamlessly store and synchronize data between the cloud and the devices they use. Users can create, open, and edit files without impacting their existing workflows while OneDrive synchronizes those changes in the background. Users can access their files from any device using their Microsoft account.

Historically, it's the user's responsibly to set this up. Known Folder Move enables IT to facilitate OneDrive to begin protecting the commonly used Desktop, Pictures, and Documents folders.

Enabling Known Folder Move is done through Group Policy. You'll need to install the Group Policy templates, which are located at **%localappdata%\Microsoft\OneDrive[BuildNumber]\adm** of a OneDrive client. You'll need to enable the **Prompt users to move Windows known folders to OneDrive** policy and configure it with your tenant ID (located in Microsoft Entra admin center).

![Screenshot of the user experience when Known Folder Move is implemented.](https://learn.microsoft.com/en-us/training/wwl/plan-transition-modern-endpoint-management/media/known-folder-move-b78855c6.jpg)

If a user is already using OneDrive to redirect their folders to another account (such as a personal account), they'll be prompted to direct the folders to the organizational account.

Alternatively, you can also configure this to occur without any user interaction. Enabling the **Silently move Windows known folders to OneDrive** group policy with your tenant ID if you don't wish to prompt users to migrate folders to OneDrive. You can also decide whether to show a notification when folders have been redirected.

There are some considerations to consider when choosing to use Known Folder Move:

- You can’t use KFM if you're using Windows Folder Redirection for Desktop, Pictures, or Documents folders.
- Consider configuring the sync client upload rate GPO if you have a large organization or expect KFM to result in a large amount of data being migrated. Also consider a pilot group to assess potential impact to network traffic.
- KFM will return errors if unsupported conditions are found. These can include unsupported file types (such as Outlook or OneNote files), exceeding maximum path length and known folders not in the default locations.

Utilizing OneDrive Known Folders compliments ESR and allows the ability to manage Win32 application settings without the need for legacy roaming profiles.

### Integrate USMT with Configuration Manager

To migrate settings from one device to another or retain settings on the same device during a rebuild process also known as a **Hardlink migration store**, you can utilize USMT (User State Migration Tool) on a single device. Configuration Manager offers several components of USMT that can be used for this purpose. In this section, we'll explore some of the available options and provide an example of how you can effectively utilize USMT in real-world scenarios.

After setting up the Configuration Manager site, one prerequisite of the Windows ADK is the installation of the User State migration components. This enables Configuration Manager to create and integrate a USMT package. Below outlines at a high level the key components involved.

#### Create a USMT Package from Configuration Manager

After installing the prerequisites, you can either create a custom USMT package or use the default package to manage the capture and reinstatement of data. Typically, you'll copy the default package and then replicate it to include the changes related to the use scenario. You can use either package in the process.

The default package is located on the Configuration Manager site server under:

%Program files%\Windows Kits\10\Assessment and Deployment Kit\User State Migration

#### Set up a State Migration Point (Configuration Manager Site System Role)

To support multiple migrations of user data during an upgrade, you can assemble a State Migration Point (Configuration Manager Role) to act as a file share to store data. Each request stores a unique hash relating to the device that allows data to be captured (through a computer association), the device upgraded, and the relevant data reinstated afterwards. For large enterprises, it's common to have regionally located State Migration Points within the site hierarchy.

#### Task sequence

Task sequences play a crucial role in managing the entire OS deployment process, allowing you to incorporate USMT when necessary. USMT is utilized at the initial stage of the process to capture user settings, and it can also be used as a post-build step to restore those settings for specific users based on the chosen options. The USMT package, created during site setup, is then referenced within the task sequence steps to enable this functionality.

#### USMT templates used for migration

USMT templates consist of four .xml templates that control data, which is collected. These files are:

- MigApp.xml
- MigDocs.xml
- MigUser.xml
- ConfigMgr.xml

These four files provide the means to customize the data collection process for a user's profile. By creating custom versions of these files, you can specify which specific data you want to collect, while still adhering to the XML template structure. These files are executed within either the Scan or Load module and are referenced in the Configuration Manager task sequence step.


# Migrate workloads when modern transitioning

Completed100 XP

- 3 minutes

For organizations currently using Configuration Manger, there are obviously choices an organization must make with regard to how they'll leverage Endpoint Manager. There's no "correct choice" to transitioning to modern management; organizations must choose which solution within Endpoint Manager best fits the various scenarios they face. Microsoft fully supports Endpoint Manager, and that includes all the capabilities that Intune and Configuration Manager provides.

### Migrate client management to Intune

When an organization has completely moved client devices from legacy OS versions, an organization may consider shifting to managing their clients completely using cloud-based management. Configuration Manager requires a certain level of expertise to maintain the on-premises infrastructure and reducing or eliminating that layer of complexity can simplify administration efforts.

Smaller organizations should consider moving to 100% cloud-based management if:

- The OS configuration capabilities provided by Autopilot meet deployment needs.
- Applications are modern and relatively simple installs.
- There isn't an excessive number of existing legacy applications.
- The existing configuration management deployment is relatively simple.
- Server management requirements can be accomplished with other tools such as Windows Admin Center.

### Choose workloads within Endpoint Manager

Larger organizations may want to continue using Configuration Manager and leverage co-management in Endpoint Manager. This isn't as much about the number of devices; it's more that enterprise organizations tend to have more complexity in their infrastructure, legacy systems and applications, or requirements that Configuration Manager is best suited to handle.

Enterprise organizations that have been using Configuration Manager for years also have a significant time investment in its existing configuration. For example, an organization can have several hundred application packages and extensive settings and compliance policies. Even if Intune addresses all the needs that Configuration Manager currently manages in an organization, the effort to migrate that to Intune would be significant. Customers shouldn't arbitrarily migrate workloads unless there's a clear value to be gained by shifting those workloads.

However, there may be some workloads where there's a clear value to migrating them. OS deployment is a common example. Image management is typically an ongoing effort that is tedious and time consuming. As most new devices come with Windows 10 or Windows 11, organizations frequently see immediate returns by adopting Autopilot to replace image deployment. Applications, like Office, and new applications can be deployed through Intune (which are typically easier to perform) while existing and complex applications can be deployed with Configuration Manager. The Endpoint Manager Admin Console helps unify the management of the device, while still providing choice as to which underlying technology to use for delivery.

