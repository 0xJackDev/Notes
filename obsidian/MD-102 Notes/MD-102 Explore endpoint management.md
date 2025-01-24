## Objectives

Microsoft 365 Is a cloud based suite of applications like Microsoft word, OneDrive, Microsoft Teams, Outlook and more Basically Microsoft 365 is all of Microsoft's products into one.

Microsoft Entra is a unified Identify and Access management (IAM) solution developed by Microsoft designed to help organization secure identies across cloud, Hybrid or on premises resources. Entra enables organizations to magage who has access to what Under what circumstances and ensure most people have it. This is The rebranding of Azure Active Directory. 

After completing this module, you'll be able to:

- Describe the benefits of Modern endpoint management.
- Explain the enterprise desktop lifecycle model.
- Describe considerations for planning hardware strategies.
- Describe the steps in planning OS and app deployment.
- Describe considerations for post-deployment and retirement.

- EMM Solutions (enterprise Mobility management)
Modern Endpoint management is a novel approach to managing windows, similar to managing mobile devices using Enterprise Mobility Management (EMM) Solutions. This allows you to simplify deployment and management and Improve security so now you can manage devices of all kinds including Desktops, HoloLens, Surface Hubs, Company Owned devices and employee owned devices EVEN MOBILE DEVICES RUNNING IOS OR ANDRIOD. All using one EMM solution


- Easy to deploy and manage compared to Operating system deployment (OSD) which is typically complex and time-consuming. 
- There's now a more straightforward way to provision new Windows devices. Windows Autopilot, deeply integrated with Microsoft EntraID and Intune simplifies and personalizes the out-of-the-box (OOBE) user experience. Windows autopilot joins the device to Microsoft Entra ID and enrolls it in Intune which automatically applied users email, apps, files and prefences and organization security settings.

- Always Making sure you are up to date with Security threats Requires changing how windows and Microsoft 365 apps need to be updated. Powerful insights driven by cloud intel and a Modern EMM approach with Enterprise mobility please Enterprise Mobility Security (EMS) Insures there is a better way to keep devices up to date.

- Intelligent Security Built in. Microsoft 365 was designed with security in mind. Microsoft built so many new growing security features directly into the Microsoft 365 platform including Windows Hello, Windows Defender Advanced Threat Protection, Windows Information Protection, Microsoft Entra Identify Protection, Conditional access and more. These security features powered by Microsoft's Intelligence security Graph. Works with Machine learning 




## Enterprise desktop Life Cycle


Organizations constantly manage the different phases of the enterprise desktop life cycle. These phases include:

- **Planning:** Preparing defining a strategy for system management.
- **Purchasing:** Processing requisitions, and then obtaining approval of invoices for payment.
- **Deployment:** Installing an operating system, enrolling devices, and deploying applications to the device.
- **Operations:** Ensuring that systems are functioning properly and are protected.
- **Support:** Ensuring that the end users learn how to use their systems and applications, and receive the support they need.
- **Upgrade and Retire:** This phase includes replacing devices, retiring obsolete hardware, or unenrolling a device from the organization.

![Illustration of a life-cycle progression, which starts with a list to represent planning, and an arrow pointing from the list to a money icon to represent the purchase of a new system. An arrow points from this icon to a computer, which represents deployment. From the computer, an arrow points to a user operating a computer, which represents operation. An arrow points from the user to an icon of a person with some tools, which represents support. From this icon, an arrow points to an icon of a computer with a CD next to it, which represents upgrading. From this icon, an arrow points to an icon of a computer with a red X on it, which represents retirement.](https://learn.microsoft.com/en-us/training/wwl-azure/explore-enterprise-desktop/media/enterprise-desktop-lifecycle-9e6e379b.png)



## Planning and Purchasing

Before Making decisions about purchasing. Organizations should carefully plan their requirements for new systems. Most organizations have a mix of old and new devices. They can replace some o these devices with new equipment and upgrade others to Windows 11. Upgrades require planning to make sure they work right. During upgrade process correct any previous OS misconfigurations.

The Planning stage includes:

- **Computer strategy:** This planning stage includes policies such as image and hardware standardization, environment design, replacement frequency, mobile device versus desktop usage, and Bring-Your-Own-Device (BYOD) policies.
- **Computer selection:** This process involves choosing hardware, software, and peripherals. It includes design configuration and application compatibility testing.
- **Deployment methods:** Each deployment method includes inherent costs to support that method. Often, IT professionals can use multiple deployment methods to accommodate different scenarios. You should determine whether a cloud-based solution addresses your deployment requirements or what requirements you needed for a device to enroll.
- **Demand forecasting:** This stage is the organization’s attempt at predicting its future computing resource requirements to determine the resources it needs to purchase.
- **Design configuration:** This process determines which new features you use and how to incorporate them into the overall plan. The new tools, resources, and settings can dramatically simplify configuration processes.


Purchasing involves getting personnel, material, services or property from a vendor through allows means. Its the action or process of acquiring items at the operation level. The purchasing process includes negotiation contract, vendor managment, shipping and disposal of packaging materials 


During the Purchasing stage, several decision points affect the overall cost of the deployment:

- **Hardware:** Hardware typically represents approximately half the costs in the purchase phase of the computer life cycle.
- **Software:** Software costs include productivity applications, antivirus software, and communication tools.
- **Accessories:** Accessories include various computer-related supplies, such as cables, power supplies, keyboards, mice, laptop bags, docking stations, and secure-access cards.
- **Deployment process:** The chosen deployment method will directly affect the overall deployment cost. Additional costs can include storage requirements of file servers and hard disk drives, USB flash drives, and providing greater bandwidth for pushing large images and user data across a network.
- **Hardware staging:** After the systems arrive, you must prepare them for deployment. This process includes securely and adequately storing, unpacking, inspecting, and inventorying the systems. You should set aside the necessary space for staging the newly purchased hardware before it arrives.




## Desktop Deployments.

The desktop deployment life cycle provides a framework for the tasks required to deploy a software application or operating system successfully. It would be best if you understood the lifecycle phases to properly plan for the resources and tools needed for effective implementation. The critical phases of the desktop deployment lifecycle are Building and Deploying.


These steps include

1. Building
2. Deployment
3. Enrollment
4. Data Migration



Lets talk about Building first.
- This phase allows you to improve efficiency when developing a strategy for a Base OS configuration its key the steps include
- 1. Streaming the Deployment process which includes developing automated solutions and procedures that you can use for deployment
- 2. Developing the deployment process which traditional might include a Baseline OS image. Using newer features like Windows autopilot might involve creating a base device configuration 
- 3. Testing: With a test system Identify and correct errors before deployment. Many people use Virtual machines
- 4. Configuration which includes Developing a automated solution and testing and configurating standard images or device configs account for the IT labor to configure computers and planning network access
- 5. Managing the logistics: this step includes storing computers, deploying and setting up physical hardware and communicating to end users. This step can also include providing the hardware vendor with configuration access.


Lets take about deployment:
After you built and test your baseline OS, you can begin deploying them and ensure theyre stable and usable. A typical  Deployment takes place in phases throughout the networking environment. The deployment team stabilizes each phase before progressing to perform upgrades or installations. Use early phases to validate scenarios such as device configuration profiles, Image configurations and more. 



### Enrollment

With enrollment, there’s no operating system deployment. The existing device becomes a recognized entity within the organization and can access resources. For devices that already have Windows 10 and later, modern methods don't require the OS to be redeployed to configure the device. Instead, the device is reconfigured to the organization’s requirements by enrolling the device and using Windows Autopilot.

You can also use enrollment for mobile devices and the support for bring-your-own-device (BYOD) scenarios. The scenarios supported can range from accessing e-mail utilizing the user’s personal device to deploying organizational applications and complete management of the device.

Each organizational group within each use-case scenario might have different requirements. You might have additional requirements for your use-case and sub-use-case scenarios and their associated organizational groups and mobile device platforms. You might define which devices you'll support and the minimum required configurations to access a resource. For example, your organizational device requirements might require devices to enroll with a more restrictive set of device settings, like a PIN of 6 characters or disabled cloud backup. BYOD scenarios might be less restrictive and allow a four-character PIN and cloud backup.



### Data Migration

Even with a successful deployment, data loss is almost always unacceptable. Many organizations are moving to cloud solutions, such as Microsoft 365 or OneDrive, to minimize or even eliminate the need for data migration. Organizations should ensure users are aware of and use the supported options. It would be best to consider scenarios where cloud solutions aren’t available or feasible. There are several solutions available that this course will cover, but it’s important to understand that data is a critical part of the process. When planning for data during a deployment, some best practices are:

- **Migrate essential data to a cloud or non-local solution before deployment:** It's generally easier and safer than continuing the risk and solving the problem after migration. Tools like Known Folder Move (KFM) can help seamlessly migrate local data to the cloud. When cloud solutions aren’t feasible, consider migrating data to network file shares or work folders. You can use features like _Enterprise State Roaming_ to migrate common settings.
- **Use in-place upgrades when possible.** This process is the recommended practice for deploying upgrades. While re-imaging devices were historically recommended in the past, this is only the case today if there’s a scenario where in-place upgrades aren’t supported.
- **Use the User State Migration tool** The User State Migration Tool is used when local data or application settings migration is necessary. You can use User State Migration Tool (USMT) 10.0 to streamline and simplify user state migration during large deployments of Windows operating systems. USMT captures user accounts, user files, operating system settings, and application settings and migrates them to a new Windows installation. You can use USMT for both PC replacement and PC refresh migrations.




## Plan an application deployment

Application deployment planning consists of three phases: managing application inventory and compatibility, packaging applications, and providing life-cycle support.



Application compatibility can have a far-reaching impact on your organization. You can significantly reduce that impact by adequately planning your application compatibility project. Updates to Windows rarely affect application compatibility; however, they can happen. Most applications will function as expected when upgrading from a previous OS, such as Windows 10, to Windows 11. However, there are typically always some applications (such as Anti-virus) that will require attention.

Gathering an application inventory is the first step in understanding the effect of application compatibility changes in your environment. Microsoft offers tools to perform asset inventories, such as the **Microsoft Intune Suite**. For environments with thousands of managed applications, you can undertake an application compatibility project to reduce the number of applications in the environment, which will reduce the costs associated with application proliferation. An easy, immediate way to reduce the number of applications within an environment is to standardize the application versions across an organization.




### **Application packaging**

Application packaging and automated installation involve using silent installation commands from vendors. You can find these commands in installation guides, on Internet forums, or by launching the setup application with the /help or /? Command-line options. Silent installation commands might not be available for applications that you develop in-house. If this occurs, you'll either need to package or repackage those applications if the installer package doesn't work. You can create Windows Installer packages. Microsoft Application Virtualization (App-V) provides a packaging mechanism with the application sequencing it uses to create virtual applications.


### **Application life-cycle support**

Application life-cycle support usually involves deploying new applications, installing new versions of existing applications, and updating applications.

- **Deploying new applications:** It's best practice to test new applications for compatibility issues with existing applications.
- **Installing new versions of existing applications:** Version upgrades are usually significantly more complex than updates, and comprehensive planning and testing are fundamental to ensuring that the upgrade release occurs appropriately.
- **Updating applications:** Updates are far more frequent and require less testing than version upgrades.

### **Application Delivery**

Organizations have several options for choosing how to deliver applications. Applications can be installed automatically (such as during deployment, based on user group memberships) or through a portal where users can install applications On Demand. It would be best to consider whether the organization will support access to applications and data on personal devices. Most common scenarios include accessing work e-mail using Outlook on a mobile phone. Still, they can also have the ability for users to install line-of-business (LOB) apps on personal devices.

### **Microsoft Intune**

Microsoft Intune is a suite of centralized device deployment and management tools. Customers can manage their app deployments using Microsoft Intune. Intune supports a wide variety of application installation types. These deployments include common apps such as Office, application package deployment, line-of-business (LOB) apps, and curation of built-in apps. Intune also supports application policies to protect data in BYOD scenarios and ensures that only devices that meet compliance rules can access application data.

### **Virtual Application Delivery**

Virtual application delivery can be beneficial when the client can't run the application. Applications are installed on a server or Cloud PC and delivered remotely. Azure Virtual Desktop and Windows 365 can provide a client desktop experience. These solutions are excellent in scenarios where installing the application could be more practical or desired, such as providing temporary access to a contractor.


# Plan for upgrades and retirement


At some point, you might have to decide whether to upgrade or retire company hardware. Several factors will help guide your decision on whether to upgrade or retire a system and purchase net new. First, you must decide whether upgrading is necessary. You base this decision on factors such as the age of the current computers, their performance, and the cost of upgrading compared to continuing to use them.

In most cases, consider the following factors:

- You'll need facilities to store systems undergoing refurbishment and a place to store them until you return them to the user’s workspace.
- You can upgrade software in place at a user’s workstation. However, upgrading an application to a new version requires more planning and testing than managing an update.
- Some organizations have procedures to refurbish used equipment and test stock items before deployment or after users return them. New employees might need fully equipped computers to perform their duties.


### **Retirement**

The retirement phase is an issue that every organization must eventually face. This phase focuses on successfully removing a system from production when it's no longer useful. As you retire legacy systems and replace them with new systems, you must efficiently complete this effort without interrupting daily organizational business needs or end-users work. Eventually, all software systems become obsolete, or other systems supersede them. Hardware systems undergo upgrades, but sometimes you no longer require and should remove them.

Other factors that you must consider when planning the retirement phase include:

- IT professionals should perform computer pickup in a way that causes the least interruptions to users. Typically, you can do this during non-business hours by going to each department or room to retrieve computers. IT departments usually coordinate pickups with the distribution of new systems.
- Like your refurbishing efforts, you should also prepare computers for reselling. If systems will go to an outside entity, ensure that sensitive information stored on hard drives and other magnetic media doesn't travel outside your organization. As part of the retirement process, you should typically remove the data stored on drives. You can use many software tools to do this, and some machines can erase drives in bulk, even if the drives aren't operational.
- Your organization might require administrative processing, which refers to the paperwork necessary to inventory and account for all computer equipment removals and sales. You can accomplish this with an existing inventory system.
- You might need to perform packing and shipping and a loading-dock area for pickups.
- It would be best to consider the equipment’s residual or resale value for accounting. For example, companies assign laptops at a higher price than desktops. Some organizations give old equipment to charity and use such donations as part of their overall tax accommodation.

### **BYOD and Unenrollment**

In BYOD scenarios, users might either replace their devices or leave the organization. The IT department must consider how to address organizational data and applications on the user’s device. They can completely wipe a device, removing all accounts, data, policies, and settings. This action is performed when the device is no longer used or lost. However, in BYOD situations, users will typically not accept IT wiping the device if they leave the company, as they would also lose their personal information.

Services like Microsoft Intune can selectively wipe and remove applications and application data. However, these applications must be managed and support these capabilities. The platform, such as iOS, Android, or Windows, can also be a factor. It would be best if you considered how to remove applications and data before granting access to them. Regardless of which methods you choose for data removal, users should know policies before enrolling devices.



This module discussed how the enterprise desktop lifecycle has changed over time and the difficulties IT professionals encounter while managing and supporting it. It introduced modern endpoint management methods necessary for deploying and maintaining desktops in a constantly changing environment.

This module explained the enterprise deployment lifecycle, which comprises planning, acquiring desktops, deploying them, managing them after deployment, upgrading them, and retiring them.

Now that you've completed this module, you'll better understand the benefits of:

- Modern Endpoint Management.
- The desktop lifecycle model.
- Hardware upgrade strategies
- Planning for operating systems and application deployment
- Considerations for post-deployment and retirement