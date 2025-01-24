In this module, you're introduced to managing apps on Intune managed devices. You'll learn how to manage apps on non-enrolled devices. You're introduced to the various options you have when deploying Microsoft 365 Apps, such as Intune, Configuration Manager, and manually,

The module concludes with an overview of how to use IE Mode with Microsoft Edge. Lastly you learn how to track your installed applications, licenses, and assigned apps using Intune.

### Objectives

After this module, you should be able to:

- Explain how to manage apps in Intune.
- Understand how to manage apps on non-enrolled devices.
- Understand how to deploy Microsoft 365 Apps using Intune.
- Learn how to configure and manage IE mode in Microsoft Edge.
- Learn about app inventory options in Intune.



# Manage apps with Intune

Completed100 XP

- 3 minutes

Intune application deployment procedures entail several considerations and settings to ensure that a deployment is successful. No matter what type of app you're deploying with Intune, the overall process is the same.

![Diagram of the app deployment steps with Intune.](https://learn.microsoft.com/en-us/training/wwl-azure/administer-endpoint-applications/media/app-deployment-c52a07de.png)

To deploy an app from Intune, perform the following steps:

1. **Ensure that Intune supports the app:** Make sure that Intune supports the application installation type and that the application can be installed without user intervention.
2. **Create Microsoft Entra groups for either users or devices:** In Intune, you create user-based or device-based groups to help you target software management tasks to specific users or devices. If you have a specific group of users that requires an application, create a user or device group for the app deployment. If you’re planning to deploy available installations, you also should link managed users to their computers to ensure that external links and company portal apps are available.
3. **Add the app to Intune:** You must upload LOB apps to Intune cloud storage, specify a URL for web apps, or link a store app to Intune. For LOB apps, you must configure installation requirements, detection rules, command-line arguments, and provide general information about the app. Adding the app makes it available for deployment from the Apps section in the Microsoft Intune admin center console. Assign the app to user or device groups. When you create an application, you can assign the app to a set of users or devices. Once assigned, the app can either be installed by the user or, if the device is managed with Intune, the app can be automatically installed.
4. **Configure policies:** You can manage application features and protect data by deploying app configuration and app protection policies.
5. **Monitor the results of the app deployment:** You can monitor the status of app deployments and installations from the Intune console by viewing the details for any app that appears in the list of apps in your Client Apps blade. You can view the installation status for the app either by device or by user.

#### App categories

A common setting across app types is **Category**. When you add more than just a few apps, organizing apps in the Company Portal into groups is helpful for your users. Creating categories allows you to do this in a way that makes the most sense for your organization. There are already nine categories created for you in Intune. You can assign apps to one category, multiple categories, or no categories.

To create your own app categories in Intune, perform the following steps:

1. On the **Apps** page, select **App categories** under **Other**.
2. Select **Add**, and enter a name for the category in the **Name** field, and then select **Create**.

#### Assign apps

You can assign the app to users and devices either when adding the app to Intune or afterwards. Assigning apps makes them available for users to install or can cause the app to be installed automatically. You assign the apps to Microsoft Entra groups, this can be either user groups or device groups; for each group, you choose an assignment type. The assignment type will differ depending on the app type you choose to assign.

When you assign apps by using Intune, you have the following options in the **Assignments** tab:

- **Available**. The app is available in the Company Portal, and users can install the app.
- **Not Applicable**. The app doesn't install and doesn't appear in the Company Portal.
- **Required**. The app installs automatically on a device in the selected group.
- **Uninstall**. The app uninstalls automatically from a device in the selected group.
- **Available for enrolled devices**. The app is available to users who have devices enrolled in Intune.
- **Available with or without enrollment**. The app is available to users who don't have devices enrolled in Intune.

Although you assign apps to either devices or to users, the options for how you can assign them will depend on the enrollment status of the devices with Intune. The following table shows you the assignment options when a device is enrolled in Intune and when it isn't enrolled. It also shows the options users have, depending on the device enrollment.

Expand table

|**Options**|**Device enrolled in Intune**|**Device not enrolled in Intune**|
|---|---|---|
|Assign an app to a user|Yes|Yes|
|Assign an app to a device|Yes|No|
|Assign an app using the Intune SDK|Yes|Yes|
|Assign an app as Available|Yes|Yes|
|Assign an app as Required|Yes|No|
|Uninstall an app|Yes|No|
|Receive app updates from Intune|Yes|No|
|User install of an app from the Company Portal app|Yes|No|
|User install of an app from the Company Portal website|Yes|Yes|

# Manage Apps on non-enrolled devices

Completed100 XP

- 3 minutes

Many ways exist today for you to make applications available to your users. Intune can supply them as either Required or Available, or users can get them right from public stores.

Apps downloaded from public stores are unmanaged, while those assigned by Intune are managed. For managed apps, IT has direct control over deployment, ongoing management (such as inventory or updates), and selective wipe of the apps and their associated data. Most mobile devices have OS level controls to limit (containerize) data movement. Intune supports an additional management level for managed apps integrated with the Intune App SDK or the Intune App Wrapping Tool. Additional controls, such as per-app PIN, jailbreak detection, and granular control over data flow can be added for these MAM-protected apps. Depending on the specific DLP requirements of your organization, you can choose the right mix of unmanaged, managed and MAM-protected applications for your users.

An unmanaged app is any app available on Windows, Android and iOS. Intune doesn't have any control over the distribution, management, or wiping of these apps. Intune MAM provides additional capabilities to protect managed apps by offering an additional layer of data protection.

A managed app is an app for which Intune manages the whole lifecycle such as:

- Deploy the app
- Manage app updates
- Monitor app installation
- Selectively wipe the entire app

Intune also supports deploying apps to unenrolled devices. Currently, you can assign iOS and Android apps and iOS and Android built-in apps to devices not enrolled in Intune.

#### Updates for unenrolled devices

To receive app updates on devices not enrolled with Intune, device users must go to their organization’s Company Portal and manually install app updates.

Users can then use either the Company Portal app or go to the Intune Company Portal website at [https://portal.manage.microsoft.com](https://portal.manage.microsoft.com/) on any of their devices and install the application without needing the device to be enrolled in Intune. The Company Portal app will only prompt users to enroll their devices if the app is configured to require enrollment.

#### Deploy apps to unenrolled devices

To deploy an app to an unenrolled device, perform the following steps:

1. Sign in to the **Endpoint Administrator admin center**.
2. Select **Apps**, then select **All Apps**.
3. In the **All apps** view, select an existing application that support assignment to unenrolled devices.
4. On the Overview page of the selected app, select **Properties**.
5. On the **Properties** page, next to the **Assignments** section, select **Edit.**
6. On the **Edit Application** page, under **Available with or without enrollment**, select **+Add Group** or **+Add all users**. You can select the groups to which you want to assign the app. You must choose a group, which only contains users when assigning apps to unenrolled devices. You can also choose whether to make the app available to all users, regardless whether their devices are enrolled in Intune. This will assign the app to all users in Intune.
7. Select **Review + Save** and then select **Save**.

You can easily make apps available on devices that can’t enroll in Intune and use app protection policies (MAM) to manage the apps after you install them. Even though this can be helpful in BYOD scenarios, we recommend that you always enroll your devices in Intune whenever possible, and this will give you all of Intune’s management functionality.



You have the option of installing Microsoft 365 Apps from Intune using the Microsoft 365 app type. This app type makes it easy and convenient for you to assign Office apps to devices you manage that run Windows client or macOS. You don’t need to download the installation files as they're already present in Intune. You can also install apps for the Microsoft Project Online desktop client and Microsoft Visio Pro for Microsoft 365, if you own licenses for them. The apps that you want are displayed as a single entry in the list of apps on the Intune console.


# Additional Microsoft 365 Apps Deployment Tools

Completed100 XP

- 3 minutes

Even though Intune offers a simple and easy approach for installing Microsoft 365 Apps on Windows and macOS devices other deployment options may be needed depending on your requirements.

If you need complete control of the Microsoft 365 Apps deployment, you can choose what deployment tool to use and whether to install the Office files directly from the cloud or from a local source on your network. You have the following options for preparing and deploying Microsoft 365:

- Configuration Manager
- The Office Deployment Tool
- The Office Customization Tool
- End-user installation

#### Configuration Manager

Configuration Manager is usually a good choice for organizations that already use it to distribute and manage software. Configuration Manager scales for large environments; enables extensive control over installation, updates, and settings; and has built-in features for deploying and managing Office.

#### Use the Office Deployment Tool

For organizations that don't have Configuration Manager but still want to manage their deployment, the Office Deployment Tool (ODT) can be used. You can use the ODT as a standalone tool or you can use it to download installation files that can be deployed using Intune or a third-party software deployment tool. In either case, the ODT provides rich control over installation, updates, and settings.

#### Use the Office Customization Tool

Another option is to use the Office Customization Tool. With this new web-based tool you can easily customize the deployment of Microsoft 365 Apps and other Select-to-Run managed Office products using a simple, intuitive, and web-based interface. The tool is an Azure-based cloud service, which allows you to create XML configuration files that are used with the Office Deployment Tool. In the past, you needed to create the configuration files in Notepad or another text editor. The Office Customization Tool makes this part of the deployment process easier and less likely to introduce errors.

This tool provides a simple experience, which allows you to create a configuration file for use with the Office Deployment Tool, for scenarios where you need to customize the installation of Microsoft 365 Apps. Common scenarios include:

- Initial installation of Microsoft 365 Apps and Office 2021 suites, with the ability to include standalone products such as Visio and Project and various language packs.
- Adding additional products after the initial installation of the Office suite.
- Adding additional language packs by configuring a ‘Language Only’ configuration after the installation of the Office suite or standalone products
- Standalone installation of Microsoft 365 Access Runtime.
- Installation of volume licensed products with automatic KMS and MAK activation.
- Automatic removal of previous MSI based Office products.

You can also use the Office Customization Tool to alter existing config files. This tool is helpful when you have to change the Office setup on already-installed and setup devices, or if you're creating a second or third setup and want to use your own baseline. Use Import to select the config file you want to adjust, alter it as you need, then Export to get a new config file.

#### End-user installation

Your users can download Microsoft 365 apps from the Microsoft 365 portal. This method involves the least amount of administrative preparation, but furnishes you with the least amount of control over the deployment. You can still decide how often your users get feature updates. Users need to have admin rights on their devices for this option.


### Microsoft Edge with IE mode

To overcome the hurdle of supporting legacy web applications, Microsoft Edge introduced a feature called IE Mode. IE mode on Microsoft Edge makes it easy to use all of the sites your organization needs in a single browser. It uses the integrated Chromium engine for modern sites, and it uses the Trident MSHTML engine from Internet Explorer 11 (IE11) for legacy sites.

Only those sites that you specifically configure (via policy) will use IE mode, all other sites will be rendered as modern web sites. When a site loads in IE mode, the IE logo indicator displays on the left side of navigation bar. Alternatively, IE Mode can be configured to open with a standalone Internet Explorer 11 window. However, most users prefer when sites open directly within Microsoft Edge in IE mode.

 Note

Internet Explorer provided a feature called Enterprise Mode. This enabled Internet Explorer to run in a compatibility mode for web apps that were designed for older versions of IE.

### IE mode supports the following Internet Explorer functionality

- All document modes and enterprise modes
- ActiveX controls (such as Java or Silverlight). Note: Silverlight reached end of support on October 12, 2021.
- Browser Helper Objects
- Internet Explorer settings and group policies that affect security zone settings and Protected Mode
- F12 developer tools for IE, when launched with IEChooser
- Microsoft Edge extensions (Extensions that interact with the IE page content directly aren't supported.)






# App Inventory Review

Completed100 XP

- 3 minutes

Intune provides several ways to monitor the compliance status of the apps that you've assigned to users or devices in the **Apps** blade in the Microsoft Intune admin center. You can also find information about all assigned apps and determine which version of a given app that you've deployed. The following pages provide that information:

- **Apps** > **Overview** page
    
    - List of all apps in Intune and assignment status. You can select an app to get detailed information about the assignments and install status.
- **Apps** > **Monitor** > **App licenses** page
    
    - Lists apps from the Microsoft Store or Business. License information for the apps is shown in the list. You can select an app to get detailed information about the assignments and install status.
    
    ![Screenshot of the client apps - App licenses screen.](https://learn.microsoft.com/en-us/training/wwl-azure/administer-endpoint-applications/media/intune-app-licenses-5a58fecb.png)
    
- **Apps** > **Monitor** > **Discovered apps** page
    
    - Lists all apps discovered by Intune at the last Hardware Inventory time. For devices with Device Ownership marked as "Corporate", this will be all apps installed on the device. For devices with Device Ownership marked as "Personal", this will be all apps installed via the Intune Company Portal or apps installed in a Required deployment. The number of devices that a given app is installed on, is shown in the list. You can select an app to list the devices the app is installed on.
    
    ![Screenshot of the client apps - Discovered apps screen.](https://learn.microsoft.com/en-us/training/wwl-azure/administer-endpoint-applications/media/intune-discovered-apps-b59eade0.png)
    
- **Apps** > **Monitor** > **App install status** page
    
    - Lists all apps in Intune with user and device failures listed next to app. You can select an app to get detailed information about the assignments and install status. You can export this information to a CSV file by selecting **Export** and import into Excel for further processing.
    
    ![Screenshot of the client apps - App install status screen.](https://learn.microsoft.com/en-us/training/wwl-azure/administer-endpoint-applications/media/intune-app-install-status-db87bcc4.png)
    

 Note

You can export this information to a CSV file by selecting **Export** and import into Excel for further processing. This is covered later in the course.