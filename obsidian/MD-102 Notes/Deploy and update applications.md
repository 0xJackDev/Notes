

In this module, you'll learn to deploy applications utilizing Intune and Configuration Manager, two powerful management tools. You'll also explore deploying applications through Group Policy, an essential technique for controlling and managing networked systems. Lastly, you'll delve into deploying apps using Microsoft Store Apps, further expanding your understanding of diverse application distribution methods. You'll be well equipped to manage and maintain various applications across your organization by mastering these approaches.

### Objectives

After this module, you should be able to:

- Explain how to deploy applications using Intune and Configuration Manager
- Learn how to deploy applications using Group Policy
- Understand Microsoft Store Apps
- Learn how to deploy apps using Microsoft Store Apps
- Learn how to configure Microsoft Store Apps




## Deploy applications with intune


### Microsoft Intune app lifecycle

The Microsoft Intune app lifecycle begins when an app is added and progresses through additional phases until you remove the app. By understanding these phases, you'll have the details you need to get started with app management in Intune.

![Diagram of the App lifecycle.](https://learn.microsoft.com/en-us/training/wwl-azure/deploy-applications/media/app-lifecycle-white-77f5d774.png)

#### Add

The first step in app deployment is to identify the apps you want to manage and assign, and add them to Intune. You can work with many different app types, the basic procedures are the same. With Intune you can add apps written in-house (line-of-business), apps from the store, apps that are built in, and apps on the web.

#### Deploy

After you've added the app to Intune, you can then assign it to users and devices that you manage. Intune makes this process easy, and after the app is deployed, you can monitor the success of the deployment from Intune within the Microsoft Intune admin center. Additionally, in some app stores, such as the Apple and Windows app stores, you can purchase app licenses in bulk for your company. Intune synchronizes data with these stores so that you can deploy and track license usage for these types of apps right from the Intune administration console.

#### Configure

As part of the app lifecycle, new versions of apps are regularly released. Intune provides tools to easily update apps that you've deployed to a newer version. Additionally, you can configure extra functionality for some apps, for example:

- iOS app configuration policies supply settings for compatible iOS apps that are used when the app is run. For example, an app might require specific branding settings or the name of a server to which it must connect.
- Managed browser policies help you to configure settings for the Intune managed browser, which replaces the default device browser and lets you restrict the websites that your users can visit.

#### Protect

Intune gives you many ways to help protect the data in your apps. The main methods are:

- **Conditional access**, which controls access to email and other services based on conditions that you specify. Conditions include device types of compliance with a device compliance policy that you deployed.
- **App protection policies** that work with individual apps to help protect the company data that they use. For example, you can restrict copying data between unmanaged apps and managed apps, or you can prevent apps from running on devices that have been jailbroken or rooted.

#### Retire

Eventually, the apps that you deployed will likely become outdated and need to be removed. Intune makes it easy to retire apps from service.


Before you can assign, monitor, configure, or protect apps, you must add them to Microsoft Intune. The users of apps and devices at your company (your company's workforce) might have several app requirements. Before adding apps to Intune and making them available to your workforce, you must assess and understand a few app fundamentals. You must understand the various types of apps that are available for Intune. You must assess the app requirements, such as the platforms and capabilities that your workforce needs. You must determine whether to use Intune to manage the devices (including apps) or have Intune manage the apps without managing the devices. Finally, you must determine the apps and capabilities that your workforce needs, and who needs them.

You can add the following app types in Intune:

- **Store app:** Apps that have been uploaded to either the Microsoft store, the iOS store, or the Android store are store apps. The provider of a store app maintains and provides updates to the app. You select the app in the store list and add it by using Intune as an available app for your users.
    
- **Microsoft 365 apps:** This app type makes it easy for you to assign Microsoft 365 apps to devices you manage that run Windows or macOS. You can also install apps for the Microsoft Project Online desktop client and Microsoft Visio Pro, if you own licenses for them. The apps that you want are displayed as a single entry in the list of apps on the Intune console.
    
- **Web link:** A web app is a client-server application. The server provides the web app, which includes the UI, content, and functionality. Additionally, modern web-hosting platforms commonly offer security, load balancing, and other benefits. A web app is separately maintained on the web. You use Microsoft Intune to point to this app type. You also assign the groups of users that can access this app.
    
- **Built-in app:** The built-in app type makes it easy for you to assign curated managed apps, such as Microsoft 365 apps, to iOS and Android devices. You can assign specific apps for this app type, such as Excel, OneDrive, Outlook, Skype, and others. After you add an app, the app type is displayed as either Built-in iOS app or Built-in Android app. By using the built-in app type, you can choose which of these apps to publish to device users.
    
- **Line-of-business (LOB) app:** An LOB app is one that you add from an app installation file. For example, to install an iOS LOB app, you add the application by selecting Line-of-business app as the App type in the Add app pane. You then select the app package file (extension .ipa), which is uploaded to Intune. LOB app supports apps for Windows, Android and iOS. The following extensions are supported:
    
    - Windows: .msi, .appx, appxbundle, .msix and .msixbundle
    - Android: .apk
    - iOS: .ipa and .intunemac
- **Windows app (Win32):** Building upon the existing support for line-of-business (LOB) apps and Microsoft Store apps, administrators can use Intune to deploy most of their organization’s existing Win32 line-of-business (LOB) applications to end users on Windows devices. Administrators can add, install, and uninstall applications for Windows users in various formats, such as MSIs, Setup.exe, or MSP. Intune evaluates requirement rules before downloading and installing, notifying end users of the status or reboot requirements using the Windows Action Center.


The Win32 Content Prep Tool (IntuneWinAppUtil.exe) is a command line tool used to compress the Win32 app into a `.intunewin` file. The folder, install file (such as setup.exe) and output folder must be specified. Running the tool with the -h switch displays usage information.

A sample command might look like this:

Copy

```
IntuneWinAppUtil -c c:\testapp\\v1.0 -s c:\testapp\v1.0\setup.exe -o
c:\testappoutput\v1.0 -q

```

Once the Intunewin file has been created, it can be added to Intune. The steps for adding the app are as follows:

1. In the **Intune** pane, select **Client apps** > **Apps** > **Add** and select **Windows app (Win32)** from the drop-down list.
    
2. Select **App package file** and browse to the intunewin file you created to upload the package to Intune.
    
3. **Add the App information.** This will include information such as the name, description, publisher, category, owner, etc.
    
4. **Configure app installation install and uninstall commands.** This might look like the following for installing and uninstalling, respectively:
    
    Copy
    
    ```
    msiexec /p “MyApp.msp”
    
    msiexec /x “{12345A67-89B0-1234-5678-000001000000}
    
    ```
    
5. **Define the app requirements.** This might include if it’s x86/x64, minimum OS version, disk space required, minimum memory, etc.
    
6. **Add requirement rules.** These define a specific configuration to look for, such as an existing file or folder, a registry value, or a script to execute and compare against the results of the script.
    
7. **Configure app detection rules.** If the Win32 app has dependencies on other apps, the detection rule can bet set to check for information such as an MSI product code or the presence of a path/file, a registry key/value, or the results of a script.
    
8. **Configure App return codes.** This defines the result of the installation. Default values such as Success, Failure, Reboot required, and Retry are available. More codes can be created.


### Choose a solution for deploying an application

Configuration Manager and Intune offer application deployments to deliver your line-of-business applications to Windows clients. Below are the supported applications types that each can offer.

Expand table

|**Application Type**|**Configuration Manager**|**Microsoft Intune**|
|---|---|---|
|.MSI|Yes|Yes|
|.IntuneWin|No|Yes|
|Office C2R|Yes|Yes|
|APX/MSIX|Yes|Yes|
|Store Apps|No|Yes|
|Microsoft 365 Apps for Enterprise|No|Yes|
|App-V|Yes|No|


# Deploying applications with Group Policy

Completed100 XP

- 6 minutes

Windows Server 2022 and later includes a feature called Software Installation and Maintenance that Active Directory Domain Services (AD DS), Group Policy, and the Windows Installer service use to install, maintain, and remove software from your organization’s computers.

#### Use Group Policy to manage the software lifecycle

The software lifecycle consists of four phases: preparation, deployment, maintenance, and removal.

![Diagram showing the four software lifecycle phases.](https://learn.microsoft.com/en-us/training/wwl-azure/deploy-applications/media/deployment-lifecycle-edc0b417.png)

You can use Group Policy to manage all phases except the preparation. You can apply Group Policy settings to users or computers in a site, domain, or organizational unit (OU) to install, upgrade, or remove software automatically.

By applying Group Policy settings to software, you can manage the phases of software deployment without deploying software on each computer individually.

Using Group Policy to manage the software lifecycle has some advantages and some disadvantages that are important to consider. The advantages of using Group Policy to manage the software lifecycle are:

- **Group Policy software distribution is available as part of Group Policy and AD DS**. Thus, using Group Policy doesn't incur any extra costs for your organization, and is always available to implement because it’s already installed and ready for use.
- **Group Policy software distribution does not require client software, agent software, or additional management software**. IT administrators can use familiar tools to manage the software lifecycle.
- **Group Policy software distribution is quick and easy to use**. This allows for both faster software distribution and reduced IT training costs.

The disadvantages of using Group Policy to manage the software lifecycle are:

- **Group Policy software distribution has a minimal feature set**. This minimal feature set limits the ability to control aspects of the distribution such as the day and time of installation, the order of installation when deploying multiple applications, and the reboot process, such as reboot suppression or reboot windows.
- **Group Policy software distribution does not have any reporting**. Thus, you can't easily gather information such as how many computers have the distributed software, which computers an installation failed on, or which computers don't have the distributed software. This could lead to a scenario in which you deploy an update to an application and the update attempts to install on computers that no longer have the application to be updated.
- **Group Policy software distribution is limited to deployment of Windows Installer packages**. IT administrators have to convert non-MSI installation programs into MSI packages before being able to deploy the software by using Group Policy.

For larger organizations, especially organizations that have more than 500 computers, and for any organizations with specific software distribution requirements, Configuration Manager provides enterprise-level features and control. These enterprise-level features and control eliminate the disadvantages found in Group Policy software distribution.

#### How Windows Installer enhances software distribution

To enable Group Policy to deploy and manage software, Windows Server 2022 or later uses the Windows Installer service. This component automates the installation and removal of applications by applying a set of centrally defined setup rules during the installation process. The Windows Installer service installs the `.msi` package files. `.msi` files contain a database that stores all the instructions required to install the application. Small applications may be entirely stored as `.msi` files, whereas other larger applications will have many associated source files that the MSI references. Many software vendors provide `.msi` files for their applications.

The Windows Installer service has the following characteristics:

- This service runs with elevated privileges, so that the Windows Installer service can install software regardless of which user is signed into the system. Users only require read access to the software distribution point.
- Applications are resilient. If an application becomes corrupted, the installer will detect and reinstall or repair the application.
- Windows Installer can't install `.exe` files. To distribute a software package that installs with an `.exe` file, you must convert the `.exe` file must to an `.msi` file by using a third-party utility.

#### Manage software upgrades by using Group Policy

Software vendors occasionally release software updates. These usually address minor issues, such as a performance update or a feature enhancement that doesn't warrant a complete application reinstallation. Microsoft releases some software patches as .msp files. Major updates that provide new functionality require users to upgrade a software package to a newer version. You can open the GPO that deploys a software package, modify the software installation settings, and then use the Upgrades tab to upgrade a package. When you perform upgrades by using Group Policy, you’ll notice the following characteristics:

- You can redeploy a package if the original Windows Installer file has been modified.
- Upgrades will often remove the old version of an application and install a newer version. These upgrades usually maintain application settings.
- You can remove software packages if they were delivered originally by using Group Policy. This is useful if you’re replacing a line-of-business (LOB) application with a different application. Removal can be mandatory or optional.


# Explore Microsoft Store for Business

Completed100 XP

- 3 minutes

The Microsoft Store for Business platform enables you to procure apps for your organization, either individually or in bulk. You can manage apps procured in volume from the portal by linking the store to Microsoft Intune. This includes the ability to:

- Synchronize the list of purchased (or free) apps from the store with Intune.
- View the synchronized apps in the Microsoft Intune admin center and assign them like any other app.
- Synchronize both Online and Offline licensed versions of apps to Intune, with the app names being appended with "Online" or "Offline" in the portal.
- Monitor the number of licenses available and being used in the admin center.
- Prevent the assignment and installation of apps if there are insufficient licenses available.
- Revoke app licenses for apps managed by Microsoft Store for Business if the user is deleted from Microsoft Entra ID.


# Assign apps to company employees

Completed100 XP

- 5 minutes

After you've added an app to Microsoft Intune, you can assign the app to users and devices. It's important to note that you can deploy an app to a device whether or not the device is managed by Intune.

 Important

The **Available for enrolled devices** deployment intent is supported for **user groups** and **device groups** when targeting Android Enterprise fully managed devices (COBO) and Android Enterprise corporate-owned personally-enabled (COPE) devices.

The following table lists the various options for assigning apps to users and devices:

Expand table

|Option|Devices enrolled with Intune|Devices not enrolled with Intune|
|---|---|---|
|Assign to users|Yes|Yes|
|Assign to devices|Yes|No|
|Assign wrapped apps or apps that incorporate the Intune SDK|Yes|Yes|
|Assign apps as Available|Yes|Yes|
|Assign apps as Required|Yes|No|
|Uninstall apps|Yes|No|
|Receive app updates from Intune|Yes|No|
|End users install available apps from the Company Portal app|Yes|No|
|End users install available apps from the web-based Company Portal|Yes|Yes|


Currently, you can assign iOS/iPadOS and Android apps (line-of-business and store-purchased apps) to devices that aren't enrolled with Intune. To receive app updates on devices that aren't enrolled with Intune, device users must go to their organization's Company Portal and manually install app updates. For almost all app types and platforms, Available assignments are only valid when assigning to user groups, not device groups. Win32 apps can be assigned to either user or device groups. If managed Google Play pre-production track apps are assigned as required on Android Enterprise personally-owned work profile devices, they will not install on the device. To work around this, create two identical user groups and assign the pre-production track as "available" to one and "required" to the other. The result will be that the pre-production track successfully deploys to the device.