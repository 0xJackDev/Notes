

Both Microsoft Deployment Toolkit (MDT) and Configuration Manager employ a similar interface for operating system deployment. However, MDT mainly focuses on OS deployment, while Configuration Manager offers a more comprehensive solution for managing clients. This module discusses the routine tasks that administrators typically perform using Configuration Manager.

### Objectives

After completing this module, you'll be able to:

- Describe the capabilities of Configuration Manager
- Describe the key components of Configuration Manager
- Describe how to troubleshoot Configuration Manager deployments

For many organizations, Configuration Manager has been at the center of their deployment strategy. Configuration Manager capabilities provide a one-stop shop not only for OS deployments but also application management and device health.

Starting in version 1910, Configuration Manager is now part of Microsoft Endpoint Manager. Microsoft Endpoint Manager is a suite of tools that work together to unlock many of the scenarios and challenges that enterprises face in today’s world. These tools bring about a modern mindset and approach to situations that have always existed or ones that are ever evolving, such as working from home and remote management.

This unit examines how you can use Configuration Manager to support a Windows deployment. It also explores how Configuration Manager, along with co-management, helps to build the foundation on your journey towards modern management.

The following Microsoft management solutions are all now part of Microsoft Endpoint Manager:

- Configuration Manager
- Microsoft Intune
- Endpoint Analytics
- Windows Autopilot
- Other features in the Device Management Admin console


### The role of Configuration Manager in a modern desktop journey

Configuration Manager has traditionally served as an on-premises management solution, primarily focusing on the management of desktops, servers, and laptops within your network. This includes devices accessible through a DMZ if needed. However, with the emergence of modern management tools like Intune and Autopilot, along with continuous innovations to Configuration Manager itself, the product has evolved to bridge the gap between traditional and contemporary management approaches.

By integrating Microsoft Entra ID, the Microsoft Defender security stack, and the Endpoint Manager admin console, Configuration Manager now provides a unified and comprehensive management experience. This single pane of glass functionality has never been more relevant than it's today. While retaining its existing capabilities, such as application deployment, software updates, and device management, Configuration Manager gains added value when combined with Intune and co-management. This combination offers the flexibility to align the most suitable tool with the specific scenario at hand, enabling a truly modern and agile approach to management.


### The foundations of MDT

Traditionally, Configuration Manager admins have used both Configuration Manager for management and control, and the Microsoft Desktop Toolkit (MDT) for the extra value and flexibility that it brings. Prior to Current Branch (CB), some options and methods were more readily available in MDT than they were in Configuration Manager, including:

- Some of the key benefits of combining the tools include:
- Access to a wider expanse of task sequence variables with which to utilize during OS deployment.
- MDT Rules engine offers a raft of in-built options to aid OS deployment.
- The ability to install Windows features without the knowledge of code.
- Log file collection out of a template task sequence wizard.

With the advancements of Windows and Configuration Manager, along with the support of PowerShell integration, many of the previously innovative options of MDT can now be done in a different way. Many admins have chosen to use these new advancements in place of where MDT was once used.

As mentioned previously, when planning and strategizing your OS needs, the scenario and deployment methods you use should dictate the toolset you select rather than using them simply because they were always used. An array of tools exists across MDT and Configuration Manager, and these decisions will help you plan, which is the most appropriate to use. When deciding whether to combine MDT and Configuration Manager, it's important to consider an organization's specific needs. This will help determine whether using one tool or both is the best choice for the Desktop admin.

### Configuration Manager overview

Configuration Manager offers a raft of capabilities, most of which fit into a deployment strategy in some shape or form. Many enterprises use Configuration Manager for its 'Single Pane of Glass' methodology to maintain devices, whether this is the delivery of the OS and applications, or the servicing and management of the device. The 'Single Pane of Glass' methodology brings disparate systems together into one system.

With the use of co-management for the modern transition and the Endpoint Manager console, the ever-evolving sync between the two has made the investment in Configuration Manager even more valuable. Some of the key elements that Configuration Manager Current Branch offers (as of CB2010) include:

- OS Deployment
- Application Management
- Update Management
- Servicing Management
- Device Inventory (CMDB)
- Basic License Tracking
- Self-Service Software Catalog
- Cloud Management capability
- Real-Time query and reporting
- Enterprise Scalability
- Microsoft Entra Integration
- Proactive cadence adoption through Desktop Analytics
- Remote Control
- User Settings Capture and Restore

The introduction of a Cloud Management Gateway (CMG) has become crucial to enabling enterprises to service their clients with the recent surge in remote working, meaning this is one of the most heavily utilized modern features within the platform.


# Examine deployment components of Configuration Manager

Completed100 XP

- 7 minutes

Boot images in MDT and Configuration Manager are Windows PE images that initiate a Windows deployment, accessed through various mediums such as CD, ISO, USB or network. The boot images then connect to the deployment share to begin the deployment. Configuration Manager also allows for the creation of MDT boot images within its UI when both tools are integrated.

Configuration Manager provides two default boot images: One to support x86 platforms and the other to support x64 platforms. These images are stored in the `i386` or `x64` folders in the following share on the site server:

**\< SiteServerName >\SMS_< sitecode >\osd\boot\**

The default boot images are updated or regenerated depending on the action that you take. You can customize boot images in many ways to facilitate troubleshooting or expand capability; however, you must consider some key concepts:

- The architecture of the boot image must be appropriate for the architecture of the destination computer. For example, an x64 destination computer can boot and run an x86 or x64 boot image. However, an x86 destination computer can boot and run only an x86 boot image.
- Make sure that the boot image contains the network and storage drivers that are required to provision the destination computer.
- Insure you included all the required applications.

The Windows ADK is required as part of the prerequisites to set up a Configuration Manager hierarchy. Windows ADK loads a set of boot images based on a specific version of Windows. These images evolve as Windows does and follows a support matrix in relation to Configuration Manager site server support.

From Configuration Manager 2006 onwards, boot images have gained cloud capability, opening up new possibilities for modern deployment. However, as Autopilot and the utilization of OEM images from vendors have been introduced, the necessity of starting devices from a boot image has become less significant.

When it comes to the initial creation of boot images in both MDT (Microsoft Deployment Toolkit) and Configuration Manager, the process is similar, and the tools used for customizing the image. However, it's worth noting that the storage locations may vary. If MDT and Configuration Manager are utilized together, it's important to remember that only the boot images associated with Configuration Manager will be referenced within the Configuration Manager task sequences through the user interface (UI).

#### OS Images

Operating system images in Configuration Manager are stored in the Windows Imaging (WIM) file format and representing a compressed collection of reference files and folders that are required to successfully install and configure an operating system on a computer. For all operating system deployment scenarios, you must select an operating system image. You can use the default operating system image or build the operating system image from a reference computer that you configure.

OS images after often used for the output of a capture task sequence and where enterprises store their golden .WIM images.

#### **Operating System Upgrade Packages**

Operating system upgrade packages serve as the source files for an OS upgrade or to deliver a vanilla image. These packages are imported to Configuration Manager from a mounted ISO or DVD.

#### Device Drivers

You can install device drivers on destination computers without including them in the operating system image that is being deployed. Configuration Manager provides a driver catalog that contains references to all the device drivers that you import into Configuration Manager. The driver catalog is in the **Software Library** workspace and consists of two nodes: **Drivers** and **Driver Packages**. The **Drivers** node lists all the drivers that you've imported into the driver catalog. You can use this node to discover the details about each imported driver, to change what driver package or boot image a driver belongs to, to enable or disable a driver, and more.

Drive management is a notable subject within the deployment community, encompassing diverse strategies and techniques that aim to accomplish similar objectives. Configuration Manager empowers you to ensure the precise application of appropriate drivers to hardware, albeit in a static manner. It's equally important to regularly update these drivers or adopt a modern driver strategy as part of a long-term transition to modern management, where drivers are obtained directly from vendors rather than relying on driver packs.

#### Software Updates

Software updates in Configuration Manager provide a set of tools and resources that can help manage the complex task of tracking and applying software updates to client computers in the enterprise. An effective software update strategy is key to ensuring compliance within the enterprise and Configuration Manager allows this by building on the basic offerings of MDT and providing a management plane that can segregate updates by type or OS, and even work with existing processes for release management. Some of the components include software update groups, queries, and deployments.

#### Task Sequences

While MDT traditionally supports a lite-touch deployment (LTI), Configuration Manager takes this one step further and provides schedule-based deployments, which can be fully automated and require no user interaction. This is often referred to as zero-touch installation (ZTI), which requires the use of task sequences.

Configuration Manager supports the use of task sequences to automate several of the components in Configuration Manager. These components include software update packages, the application model (including deployment types), and more modern features, such as the Cloud Management Gateway, which open up deployment and management to remote clients.

Task sequences are defined in the Configuration Manager console. In the **Software Library** workspace, expand **Operating Systems** and select **Task Sequences**. The **Task Sequences** node, including subfolders that you create, is replicated throughout the Configuration Manager hierarchy.

Over the last several years, ZTI was the popular choice to take the headache away from the user. With the introduction of Windows Autopilot, there's now the potential for more user participation in the experience. This participation makes more options available in the deployment space and the concept of devices being shipped to a user's home and being provisioned on site is now a real possibility.



# Configuration Manager

Completed100 XP

- 3 minutes

As we've seen from MDT, you can use Configuration Manager to create and deploy Windows images to devices. While many of the concepts are similar, Configuration Manager uses its own interface to manage the import and creation of boot images and the OS images. The deployment is handled through a combination of task sequences and target collections for which objects reside.

#### Task Sequences

Configuration Manager task sequences work in a similar way to MDT task sequences, but they allow the flexibility to draw on other elements within it, such as application's created packages and scripts. In addition, you can integrate the Configuration Manager task sequence engine with the MDT binaries to offer greater flexibility around available options. Some of the scenarios for using a task sequence include:

- Deploying an operating system to a new or rebuilt device.
- Deploying a Windows upgrade.
- Capturing an operating system image for use in a deployment sequence.
- Capturing and restoring user state settings.
- Customizing a task sequence to carry out more advanced configurations.

#### Deployment Collections

Once the task sequence has been created, you have the option to direct it towards a deployment collection, ensuring its successful delivery. This serves as a safeguard in Configuration Manager, preventing the unintentional distribution of an operating system (OS) to unintended targets. You also have the option of targeting an in-built collection called **unknown computers**, which offers the flexibility of presenting any new device acquired with an ability to launch a created task sequence.

Collections help you organize resources into manageable units. Configuration Manager has built-in collections for common operations. You can also create custom collections to match your client management needs, and to perform operations on multiple resources at one time. Built-in and custom collections appear in the **User Collections** and **Device Collections** nodes in the **Assets and Compliance** workspace in the Configuration Manager console. Collections that you have recently viewed appear in the **Users** node and in the **Devices** node in the **Assets and Compliance** workspace.

By default, Configuration Manager includes the following built-in collections. These built-in collections can NOT be modified.

Expand table

|Built-in collection name|Description|
|---|---|
|All User Groups|Contains the user groups that are discovered by using Active Directory Security Group Discovery.|
|All Users|Contains the users who are discovered by using Active Directory User Discovery.|
|All Users and User Groups|Contains the All Users and the All User Groups collections. This collection contains the largest scope of user and user group resources.|
|All Desktop and Server Clients|Contains the server and desktop devices that have the Configuration Manager client installed. Membership is maintained by Heartbeat Discovery.|
|All Mobile Devices|Contains the mobile devices that are managed by Configuration Manager. Membership is restricted to those mobile devices that are successfully assigned to a site or discovered by the Exchange Server connector.|
|All Systems|Contains the All Desktop and Server Clients, the All Mobile Devices, and the All Unknown Computers collections, and all mobile devices that are enrolled by Microsoft Intune. This collection contains the largest scope of device resources.|
|All Unknown Computers|Contains generic computer records for multiple computer platforms. You can use this collection to deploy an operating system by using a task sequence and PXE boot, bootable media, or prestaged media.|
|Co-management Eligible Devices|Contains devices that meet the client prerequisites and are eligible for co-management enrollment (added in version 2111).|

 Tip

Most management tasks rely on or require using one or more collections. Although you can use the built-in collection of **All Systems**, using it for management tasks isn't a best practice. Instead, you should create custom collections to more specifically identify the devices or users for a task.

### Troubleshooting a Windows Deployment using Configuration Manager

When delivering Windows with Configuration Manager through task sequences, you may be asked to provide either statistical analysis on success rates or require an ability to do some troubleshooting. Given this is such a complex and technical process, it's inevitable something may go wrong. The following sections describe some other troubleshooting options.

#### Report

With a reporting service point configured in Configuration Manager, you can access to a set of tools and resources that help you use the advanced reporting capabilities of SQL Server Reporting Services (SSRS) and Power BI Report Server. Both reporting platforms provide rich analysis experiences for custom reports. Reporting helps you gather, organize, and present information about the wealth of Configuration Manager data in your organization. Configuration Manager provides many predefined reports in Reporting Services that you can use without changes. You can duplicate and modify the default reports meeting your requirements, or you can create custom reports.

#### Log Files

Configuration Manager produces numerous log files on both the client and server side to aid with troubleshooting. From a client perspective during the OS deployment phase, these move several times depending on the Windows Phase, but most of the time these will be located at C:\Windows\CCM\Logs. Within this directory, are several log files for helping to understand any issues that the client currently has. Some examples include the following:

- **Ccmsetup.log**. Responsible for the client setup, upgrade, and removal.
- **SMSTS.log**. Responsible for much of the initial logging during an OS deployment prior to Windows and the Configuration Manager client being fully installed.
- **AppEnforce.log**. Responsible for showcasing application installation information.
- **Execmgr.log**. Responsible for showcasing package installation information and script execution.

You can also use SetupDiag from Configuration Manager to help analyze and report on issues you may encounter during a Windows upgrade or deployment. For more information on SetupDiag, please visit [SetupDiag](https://learn.microsoft.com/en-us/windows/deployment/upgrade/setupdiag).

 Tip

A good practice is to review the SRS Reports for task sequences and review the Deployment Status report for a given task sequence. This review can act as a starting point for troubleshooting which device went wrong and where it is located.

 Tip

CMTrace is your friend for reading and interpreting logfiles. You will never look at Notepad in the same way again




# Plan in-place upgrades using Configuration Manager

Completed100 XP

- 5 minutes

Whether performed manually or through an automated process, in-place upgrade consists of using the Windows setup. The setup engine runs several small pre-installation checks, looking for known compatibility issues. It also preserves the user state and applications and only removes what isn’t compatible with the version of Windows being installed. With this option, previously installed applications and user state are preserved. In-place upgrade also allows you to roll back to the previous OS installed if needed for troubleshooting purposes.

Running setup manually isn't a scalable solution, even when using an unattended file. A task sequence is the recommended approach for large-scale deployments.

You can use both MDT and Configuration Manager to perform in-place upgrades using a task sequence. Like setup, this preserves the user’s files, apps, and settings, including the ability to roll back to the previous version if issues arise.

Until the device is upgraded to Windows 11 or later, traditional deployment tools must be used. Once the machine is upgraded to Windows 10 or Windows 11, solutions such as Windows Autopilot can be used for future servicing. This process is part of Windows Autopilot for existing devices and is covered in more detail later.

As discussed earlier, the environment and clients should be assessed prior to upgrading. Tools such as Upgrade Readiness, the Application Compatibility Toolkit, and the Windows and Planning Toolkit.

### Considerations for In-place Upgrades

The following considerations might be critical in determining whether you can perform an in-place upgrade:

- **The operating system and edition that can be upgraded to Windows**. You can upgrade to a higher Windows 11 edition, for example, from Windows 7 Professional to Windows 11 Enterprise. However, an in-place upgrade can’t migrate apps and user settings if you perform edition downgrade. For example, if you attempt to upgrade Windows 7 Enterprise to Windows 11 Pro, you'll be informed that the in-place upgrade can’t migrate any apps.
- **Sufficient hardware resources**. If a computer doesn’t meet minimum hardware requirements for Windows 11, you can’t perform an in-place upgrade. For example, if you attempt an in-place upgrade of a 64-bit Windows 8.1 computer that has 1 GB of RAM, you'll receive an error because you need at least 2 GB of RAM to upgrade to 64-bit Windows 11.
- **Windows 11–compatible hardware and apps**. If the earlier version of the Windows operating system uses device drivers or has installed apps that aren’t compatible with Windows 11, an in-place upgrade will stop and inform you about the issue. To find detailed information on these issues, you can run Setup.exe at an administrative command prompt by typing the following command and pressing Enter:

`Setup.exe /auto upgrade /compat scanonly`

Running Setup.exe creates several XML files that you can open and inspect for issues.

- **32-bit OS.** You can’t use an in-place upgrade to upgrade a 32-bit operating system to 64-bit Windows.
- **OS language**. You can’t use an in-place upgrade to change operating system languages. If you use an in-place upgrade, you must use Windows in the same language as the operating system that you want to upgrade. For example, you can’t upgrade Spanish Windows 8.1 to German Windows 10.
- **Dual boot/multiboot**. You can’t use an in-place upgrade for upgrading dual boot or multiboot computers.
- **Windows To Go/VHD**. You can’t use an in-place upgrade for upgrading Windows To Go media and computers that use virtual hard disks to start up.
- **Standard image only**. You can perform an in-place upgrade only by using the standard Windows image (Install.wim on the Windows installation media). The in-place upgrade doesn’t support using custom images because of potential conflicts between the existing apps and new apps in a custom image.

If an in-place upgrade fails in the last three phases, you can restart the device, and it will run its original operating system’s startup repair tool. This restores the original operating system and can take some time to complete.

If the upgrade path isn't supported, then an In-place upgrade can't be used. In these cases, a fresh install of the OS must be performed. This process is called an in-place migration and is discussed later in the lesson on migrating devices.



Correct. The All Systems collection contains the All Desktop and Server Clients collection, the All Mobile Devices collection, and the All Unknown Computers collection, and all mobile devices that are enrolled by Microsoft Intune. This collection contains the largest scope of device resources.