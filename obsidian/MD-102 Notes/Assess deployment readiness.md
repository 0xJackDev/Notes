

An efficient and automated desktop deployment can enable a company considerable cost savings.  TO realize this potential you must identify your organizations current software, and hardware and network infrastructure. Knowing what you can and cant upgrade is key to a proper and successful desktop deployment. 

This module provides information about some of the tools that you can use to perform detailed assessments of existing deployments, and it describes some of the challenges that you might face when performing these necessary assessments.

### Objectives

After completing this module, you'll be able to:

- Describe the guidelines for an effective enterprise desktop deployment.
- Explain how to assess the current environment.
- Describe the tools that you can use to assess your current environment.
- Describe the methods of identifying and mitigating application compatibility issues.
- Explain considerations for planning a phased rollout.




## Examine Deployment Guidelines

You can accomplish an effective deployment by implementing the following basic guidelines

- Take an inventory and establish a network map of the existing client computers, servers and other relevant networking services to determine if the installed application base and hardware types your organization has deployed. YOu should consider the organizations main operating center, Branch offices and other locations and document even small offices outside the corporate network and users working remotely from home 
- Determine what hardware you can reuse for the new computer deployment and which types you need to retire. You must fully understand the hardware requirments for a new operating system and how the system will work with existing peripheral devices like a Keyboard or monitor
- Determine which applications you can redeploy on the new desktop systems and start a process for packaging or scripting those applications so that you can reinstall quickly 
- Define a strategy for addressing applications the new platform cant support. For example using a Virtual machine might be necessary to support a Legacy application 
- Establish a process to capture user data, setting and prefences on current deployed systems to restore on newly deployed systems
- Provide a method for backing up all data from currently deployed computers before redeployment You can do this with the method above in the user data capture 
- Provide an end-to-end process for the actual desktop deployment. Several Microsoft automated systems tools can do this, all of which are covered in more detail in the next lesson.
- Create a plan for training users on the updated desktop systems. Windows's new features and functionality will help reduce troubleshooting issues significantly post-deployment.



## Explore Readiness tools


To ensure a good windows deployment you need to understand your current state is today so you can plan where you need to be after the deployment project. There are several tools to help you assess the state of your environment including identifying potential issues that can prevent deployment.


## Microsoft Intune

You can use solutions in microsoft intune to maintain compliance and control while providing employees access to the devices and applications they need to be productive. Microsoft intune provides key management capabilities in application delivery, desktop virtualization, device management, and security. Organizations using Microsoft Intune can view reports and run queries on the assets it manages, including complete inventory of the OS, software, and hardware.

## Endpoint Analytics

Endpoint Analytics is a cloud-based service that provides insights for measuring how your organization is working and the quality of the experience you're delivering to your users. Endpoint Analytics provides Windows 11 hardware readiness reports in the Work from Anywhere report. This report shows which devices are capable of running Windows 11, and lists reasons for devices that don't meet Windows 11 readiness. While Endpoint Analytics can leverage devices that are managed in Configuration Manager and co-managed devices, unlike Desktop Analytics, Endpoint Analytics doesn't require Configuration Manager.



## Assess application compatibility

An app that is written for a specific operating system may cause problems when you install it on a computer with a different operating system. Generally, apps and hardware that work on Windows 7 or 8.1 will continue to work on Windows 11 or later.


The few Windows apps that don't run in Windows 11 are primarily security-class apps (such as anti-virus protection) and apps that perform low-level kernel calls that bypass the standard Windows application-programming interface (API) and communicates with system hardware. Changes between 32-bit and 64-bit architectures and the deprecation and removal of some components that were available in earlier Windows versions from Windows 11 may also impact apps that were dependent on these features. Problems can also occur if a legacy app isn’t User Account Control (UAC)–aware, or if developers didn’t follow guidelines on how to develop Windows apps.


It's critical that you follow a set process for assessing and mitigating application compatibility issues. You must address application compatibility as an environment-wide approach rather than an unplanned activity. You can assess application compatibility with a measured and manageable process by following these steps:

1. Discover the apps that you want to continue to use in the Windows 11 environment.
2. Rationalize the apps to ensure that all discovered apps still fit into the organization’s app portfolio. If an app no longer has a practical use, you can remove it from the compatibility-assessment process.
3. Prioritize apps. Organizations might have hundreds, or even thousands of apps. It's financially and operationally impossible to test such a multitude of apps; therefore, you must prioritize your apps and decide which ones to test.
4. Test apps to ensure that the functionality that you require is available when the app runs in Windows 11 or later.
5. Mitigate any issues that you discover, which might include using built-in operating system compatibility functionality, upgrading an app, or replacing the app with one that functions properly in Windows 11 or later.

Mitigating an application compatibility issue typically depends on various factors, such as the type of application and the current support for the application.


### Mitigation methods

Some common mitigation methods include:

- **Modifying the configuration of an existing app**. Compatibility issues can sometimes require modification of an app configuration, such as moving files to different folders, modifying registry entries, or changing file or folder permissions. Tools such as Compatibility Administrator can be used to detect and create app fixes, called shims, to address compatibility issues. You should contact software vendors for information about any other compatibility solutions.
- **Applying updates to an app**. Updates might be available to address many compatibility issues, and they help an app run better on Windows 11. After applying an update, other app tests can ensure mitigation of compatibility issues.
- **Upgrading an app to a compatible version**. If a newer, compatible version of an app exists, the best long-term mitigation is to upgrade to the newer version. By using this approach, you must consider both the cost of the upgrade and any potential problems that might arise from having two different versions of an app.
- **Modifying the security configuration**. If your compatibility issues appear to be permissions-related, a short-term solution is to modify the security configuration of an app. When you use this approach, you must conduct a full risk analysis and gain consensus from your organization’s security team regarding the modifications. For example, you can mitigate Internet Explorer Protected Mode by adding a site to the trusted site list.
- **Running an app in a virtualized environment**. If all other methods are unavailable, you can run an app in an older version of the Windows operating system by using virtualization tools such as client Hyper-V.
- **Using app compatibility features**. You can mitigate application issues such as operating system versioning by running an application in compatibility mode. You can access this mode by right-clicking the shortcut or .exe file and then selecting compatibility mode from the Compatibility tab.
- **Selecting another app that performs the same business function**. If another compatible app is available, consider switching to it. When using this approach, you must consider both the cost of the app and the cost of employee support and training.

When compatibility issues can’t be solved through updates or configuration, there are several options available to facilitate continued use of an application without blocking an upgrade.




#### Application Compatibility Toolkit

Application Compatibility Toolkit (ACT) is a set of tools used during the application compatibility testing process's inventory, analysis, and mitigation phases. ACT consists of several features, including:

- A database of known application issues and mitigations for those issues.
- The Compatibility Administrator tool that can be used to create fixes for your applications to enable them to run correctly.
- A setup analysis tool that helps identify problems with application setup.
- The Standard User Analyzer that can identify issues with UAC restrictions that might affect your application’s functionality.

ACT can diagnose application compatibility issues in Windows. ACT can also solve application compatibility problems depending on the type of incompatibility issues you encounter. One of the most significant benefits of ACT is that it can provide a solution that requires no significant change to the users’ operating environment. ACT mitigates compatibility issues by attaching shims to apps. Shims redirect calls from apps to the appropriate location in Windows. They also simulate the operating system components the app is attempting to access. These fixes can be applied as part of an application’s deployment.

#### Client Hyper-V

Client Hyper-V enables you to provide a local, virtualized environment in which previous versions of Windows can run on virtual machines. This environment enables you to run incompatible apps on supported versions of Windows while maintaining Windows 10 or Windows 11 as the main operating system and using only local resources.

When choosing Client Hyper-V to mitigate potential compatibility issues, the client hardware should be considered. You must have a computer with a 64-bit processor capable of Second-level Address Translation (SLAT) to run Client Hyper-V in Windows. Because an additional OS is running, you must ensure the client has sufficient processor, memory, and disk space to support this method.

#### Remote Desktop Services (RDS)

RDS allows you to connect to a remote computer to use the computer’s resources and applications. You can set up an RDS Server Host running a version of the operating system that is compatible with specific applications. You can also allow users to connect remotely to the computer to use specific applications. You also can use Windows Server 2016 RemoteApp to provide the same functionality, except that RemoteApp runs the application inside its own window within the user’s desktop.

#### Windows 365 and Azure Virtual Desktop

The Azure Virtual Desktop and Windows 365 solutions combine RDS and Hyper-V virtualization technology to provide a more personalized and compartmentalized user experience. Instead of the client running the compatible OS in Hyper-V, Azure hosts the necessary OS. This allows administrators to implement and manage virtual machines more easily without relying on either client hardware to support running an additional OS or dependencies on the application being compatible with a server OS as RDS requires.

You can create desktop collections, which are pooled collections that users share, or dedicated personal virtual machines that you can maintain and manage similarly to physical devices.


# Prepare network and directory for deployment

Completed100 XP

- 9 minutes

It’s important to understand the capacity of the network infrastructure when planning a deployment. Without proper planning, a deployment can take longer than anticipated and drastically impact the performance of those using the network during deployment. The deployment method and the number of devices that can be deployed at a given time can be impacted by the available bandwidth and network reliability. This is an important consideration for organizations with multiple locations and wide area network (WAN) links.

When deploying an operating system or image, a primary consideration is how to deploy a large amount of data with the least amount of impact to the network. This is typically done by ensuring clients are downloading the data from the closest possible location and managing how much bandwidth is being consumed.

#### Delivery Optimization

Windows updates, upgrades, and applications can contain packages with large files. Downloading and distributing updates can consume quite a bit of network resources on the devices receiving them. You can use Delivery Optimization to reduce bandwidth consumption by sharing the work of downloading these packages among multiple devices in your deployment. Delivery Optimization can accomplish this because it's a self-organizing distributed cache that allows clients to download those packages from alternate sources (such as other peers on the network) in addition to the traditional Internet-based servers. You can use Delivery Optimization with Windows Update, Windows Server Update Services (WSUS), Windows Update for Business, or Microsoft Configuration Manager (when installation of Express Updates is enabled).

Delivery Optimization is a cloud-managed solution; therefore, access to the Delivery Optimization cloud service is a requirement. In addition, devices must have access to the internet to use the peer-to-peer functionality of Delivery Optimization.

By default in Windows 10 or later Enterprise and Education editions, Delivery Optimization allows peer-to-peer sharing only on the organization's own network (specifically, all of the devices must be behind the same NAT). However, you can configure it differently in Group Policy and mobile device management (MDM) solutions such as Microsoft Intune.

#### Branch Cache

Branch Cache replicates files from a central location to a local device like a server. Branch Cache lets clients download locally hosted data instead of consuming WAN bandwidth. Windows Server Update Services (WSUS) and Microsoft Configuration Manager can use BranchCache to optimize network bandwidth during update deployment. BranchCache has two operating modes: Distributed Cache mode and Hosted Cache mode.

- **Distributed Cache mode.** In Distributed Cache mode, each client contains a cached version of the BranchCache-enabled files it requests and acts as a distributed cache for other clients requesting that same file. This is similar to the Delivery Optimization feature in Windows.
- **Hosted Cache mode.** In Hosted Cache mode, designated servers at specific locations act as a cache for files requested by clients in its area. So rather than clients retrieving files from a latent source, the hosted cache server provides the content on its behalf.

Whether you use BranchCache with Configuration Manager or WSUS, each client that uses BranchCache must be configured to do so. You typically make your configurations through Group Policy in the **Computer Configuration/Policies/Administrative Templates/Windows Components/Delivery Optimization** node.

For detailed information about how Distributed Cache mode and Hosted Cache mode work, see [BranchCache Overview](https://technet.microsoft.com/library/dd637832%28v=ws.10%29.aspx).

#### BITS

Background Intelligent Transfer Service (BITS) is used by programmers and system administrators to download files from or upload files to HTTP web servers and SMB file shares. BITS takes the cost of the transfer and the network usage into consideration so that the user's foreground work has as little impact as possible.

BITS uses idle network bandwidth to transfer the files by increasing or decreasing the rate at which files are transferred based on the amount of idle network bandwidth available. If a network application begins to consume more bandwidth, BITS decreases its transfer rate to preserve the user's interactive experience. BITS also adapts to network interruptions by pausing and automatically resuming transfers, even after a reboot. BITS also transfers files when the machine is in Modern Standby mode and plugged in.

If an administrator enables Windows BranchCache on client and server computers in an organization through a group policy or local configuration settings, BITS will use Windows BranchCache for data transfers.

#### LEDBAT

Windows Low Extra Delay Background Transport (LEDBAT) is a network congestion control feature introduced in Windows Server 2019 to help manage background network transfers. Unlike BITS, which restricts traffic, LEDBAT consumes as much bandwidth as possible, but only unused bandwidth.

For example, an administrator might set bandwidth throttling for package downloads to 50%. With BITS alone, the remaining 50% of bandwidth isn't used, even when it’s available. With LEDBAT, an administrator can remove this throttling limitation because LEDBAT will automatically scale back as latency increases.

#### Migration data size

When many devices are being replaced or refreshed, the amount of user data to be migrated can impact device availability. End users may not be able to use their devices until their data migration is complete. If there's a large amount of data, devices may be unavailable for a longer period of time. As storage is inexpensive and client hardware typically has hundreds of gigabytes or more, user data can easily surpass the size of the OS and applications.

Organizations should first consider minimizing the amount of end user data that is stored only on the client device. Migration challenges aside, the cost and risks are higher when data is stored locally versus data that is centrally managed. Solutions such as Work Folders, OneDrive, and SharePoint enable users to work with their data as they typically do, even offline, while the data is managed and protected in a centralized location. Tied with an effective deployment solution, users should be able to move to other devices and seamlessly have access to their apps and data. This can enable the replacement or refresh process to be no more complicated than a user switching to another device.

For organizations that have either not adopted or don’t primarily use a centralized solution for user data, administrators should consider implementing such a solution prior to migrating to Windows 10 or Windows 11. This can minimize the effort involved in the data migration or device upgrade process versus implementing a centralized solution after the additional costs and risks of a migration have already been realized. Tools like Known Folder Move can help migrate a large number of users’ files to OneDrive without impacting their daily habits. Known Folder Move is examined in greater detail later in this course.

#### Directory planning

Your network directory plays a critical role in the deployment process. Organizations typically have Active Directory Domain Services (AD DS) in-place. Most organizations also use Microsoft Entra ID as it provides identity services for common cloud services such as Exchange Online and Microsoft 365. Many organizations connect their on-premises AD DS environment with Microsoft Entra ID to unify identity management across their on-premises and cloud services.

Administrators should consider using the Microsoft Entra Connect tool to integrate directories if their organizations have on-premises directories but don't currently use Microsoft Entra ID. When using modern deployment methods, setting up directory integration prior to deployment significantly simplifies the deployment process, and day-to-day management of your environment.



# Plan a pilot

Completed100 XP

- 3 minutes

When planning a pilot, ample time should be allowed to perform sufficient testing before deployment. Once testing is complete and all known issues have been resolved, the deployment should be rolled out in phases. There's always the possibility of external factors that weren't identified in the lab that can suddenly appear and impact the deployment. Even if a deployment doesn't result in any technical complications, IT staff should be prepared to support the impact of the deployment on the end users. Failure to provide sufficient resources to train users and address questions or concerns can have just as negative an impact as a software or hardware issue.

#### Phased deployment

Phased deployment using deployment rings is the concept of starting with small groups and then broadening the deployment scale in a measured way over time. Normally, when a communication and training plan is drafted, these rings and their members should be formed. This way, you can reduce potential risk and validate your approach as you continually open the deployment valve, or pause activities if needed, for example, when you see more helpdesk calls come in than expected.

Deployment rings are best created in cooperation with business units and their managers. You want an understanding of critical dates and times to avoid when deploying or making changes. With careful planning and buy-in from stakeholders, getting users on-board and comfortable with any changes coming their way will be easier.

#### Phase 1: The IT team and early adopter insiders

Begin your deployment with the IT team and enthusiastic early adopters, who volunteer for early access. With these "insiders," you can test your communications, the impacts of change, and the effectiveness of your communications and training. IT runs small pilots during this phase and learns troubleshooting and automation techniques to help during broader deployment phases.

It's important to have engaged members in the initial pilot phase, to make sure they're documenting their observations and feeding back to the process. Also, it's good to have champions outside the IT team that help extend organic, word-of-mouth communication of new capabilities, and they'll often be first line of support when users in later phases need help.

#### Phase 2: Pilot

Once you feel good about the first phase, you can target a larger set of users for your second, pilot phase. This should comprise a representative mix of user roles, device types, apps, Office add-ins, etc. Pilot devices should also be low-risk users or devices to minimize business impact during the pilot. The data returning from these groups will be used via Analytics to target the initial waves for phase 3, the broader deployment.

Remember, all PCs in this phase and future phases should be logging up to the Analytics service, so you can collect diagnostic data about device and app health as well as bandwidth savings. Endpoint Analytics can help determine candidates for pilot groups and identify potential issues that might be difficult for users to identify or neglect to report.

For this phase, it's especially important to communicate changes and help users take advantage of new capabilities. Users can often de-prioritize or ignore email or other communications coming from IT – so it helps to meet with management to get their help in communicating change and drive adoption of new tools and technology.

You'll also need their input on timeframes to avoid, so you can minimize user disruption. For example, the finance team may be sensitive at the end of fiscal quarters or product development teams during a product launch.

In parallel to planning for devices, users, departments and timing, you can start to build your communication and training plans, as well as begin compiling content or engaging outside resources to help train users.

#### Phase 3 and beyond: Broad production deployment

By reaching broad deployment phases, you'll have refined your processes, communication, training and self-service tools. Now you can use the collected diagnostic data to target more PCs.

Deploy at a manageable rate to your IT department, help desk, users and network capacity. You can always go back to Step 2 in the deployment process wheel to optimize your network further. Also be mindful of your network capacity and use optimization tools such as peer to peer cache, LEDBAT and other techniques to facilitate faster transfer of deployment-related data.

In addition to the diagnostic data you monitor via the analytics tools, you can also monitor Microsoft 365 service usage in a granular way with detailed usage reports by workload in the admin center and using the admin dashboards via Power BI. These are great tools to help set and track goals as you roll-out new tools for working together – like Microsoft Teams – or new ways to share files – like OneDrive.

New technology acceptance and adoption will go on long after every PC in your organization has Windows 11 and Microsoft 365 Apps installed. And users won't necessarily change how they work – without taking the time to inform and train them of new capabilities. Finally, communication is continual with the new servicing models providing new capabilities on an ongoing semi-annual schedule for Windows and optionally a monthly schedule for Office.