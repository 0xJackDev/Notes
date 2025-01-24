
Intune administration can be accessed using _Intune admin center_ located at [https://intune.microsoft.com](https://intune.microsoft.com/). This console includes all the management capabilities provided by Intune, but also includes common management tasks such as managing users and groups. The Intune admin center portal replaces the Intune console previously found in the Azure portal.

#### Intune Company Portal

The Company Portal is available as a web application and as an application for desktops and mobile devices on all platforms. Users use this portal to self-manage device enrollment and also to access applications that company administrator publishes. They access it via [https://portal.manage.microsoft.com/](https://portal.manage.microsoft.com/) or by installing the Company Portal app on Windows, iOS, or Android devices.

#### Device Management Lifecycle

Like most IT management activities, managing mobile devices follows a lifecycle. The mobile device management lifecycle contains four phases:

- **Enroll:** In the Enroll phase, devices register with the mobile device management solution. With Intune, you can enroll both mobile devices, such as phones, and Windows PCs.
- **Configure:** In the Configure phase, you help to ensure that the enrolled devices are secure and that they comply with any configuration or security policies. You can also automate common administrative tasks, such as configuring Wi-Fi.
- **Protect:** In the Protect phase, the mobile device management solution provides ongoing monitoring of the settings established in the Configure phase. During this phase, you also use the mobile device management solution to help keep devices compliant through the monitoring and deployment of software updates.
- **Retire:** When a device is no longer needed, when it's lost, or when it's stolen, you should help to protect the data on the device. You can remove data by resetting the device, performing a full wipe, or performing a selective wipe that removes only corporation-owned data from the device.


# Enable mobile device management

Completed100 XP

- 3 minutes

A key task of any administrator is to protect and secure an organization's resources and data. This set of tasks is called device management. Users have many devices from which they open and share personal files, visit websites, and install apps and games. These same users are also employees and they want to use their devices to access work resources, such as email and SharePoint. Device management enables organizations to protect and secure their resources and data.

Mobile device management (MDM) is an industry standard for managing mobile devices, such as smart phones, tablets, laptops and desktop computers. As a modern desktop administrator, you need to know how to manage devices in your organization by using MDM mechanism, as there are many scenarios where on-premises solutions either can't manage or might be better suited to be managed through MDM policies than traditional methods such as Group Policies.

One point of clarification – while the term "Mobile Device Manager" is used, this term is an industry term that originated from the need to manage personal phones and tablets. As modern management focuses on a unified solution for all devices, the form factor of a device, such as a desktop or kiosk that isn't necessarily mobile, shouldn't be the determining factor in whether to manage the device using an MDM.

#### Activate MDM Services

To enable the ability to support enrollment of mobile devices, the MDM Authority must be set within the Intune configuration. This is located in the Device Enrollment section of the Microsoft Intune – Overview dashboard in the portal. The default is set to None, which means the MDM isn't configured. It must be enabled by choosing the Intune MDM Authority option.

 Note

Hybrid MDM with Configuration Manager is retired. While this option may still be visible for legacy implementations, new connections to Configuration Manager cannot be created. This should not be confused with Co-Management, which is different from Hybrid MDM, and still uses the Intune MDM Authority option.

![Screenshot of the Choose MDM Authority screen.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/intune-choose-mobile-device-management-authority-1e7c6762.png)

#### Configure Intune for Apple Device Support

By default, Intune is configured to allow enrollment of Windows, Android and Samsung Knox Standard devices. To manage iOS and macOS devices, an Apple MDM push certificate is also required and must be set up in Intune.

This can be configured by going to the Intune portal, and choosing **Device enrollment** - **Apple Enrollment** - **Apple MDM Push Certificate. In this process, you will:**

- Download a Certificate Signing Request (CSR)
- Navigate to the Apple Certificate Portal (the Intune interface provides a link)
- Create a certificate by uploading the CSR and then downloading the generated certificate file.
- Returning to the Intune Portal and uploading the certificate file.

Generating a certificate file in the Apple Certificate portal requires an Apple ID that is a member of the Apple Developer program. This should be created using an account that is authorized by your organization and a personal Apple ID should never be used


# Explain considerations for device enrollment

Completed100 XP

- 7 minutes

The preferred method for managing your Windows device, which has built-in mobile device management features in the operating system, is to enroll it as a mobile device with Intune.

You must use device enrollment for devices running any operating system other than Windows, such as those on phones or Macs.

There are several different ways to enroll Windows devices to MDM, based on device type and its current state, including:

- If a device is already joined to your on-premises AD DS, you can use Group Policy to automatically enroll it to MDM.
- You can configure integration between Microsoft Entra ID and MDM so that when you join a Windows device to Microsoft Entra ID, it’s automatically enrolled to MDM.
- You can enroll Windows devices to MDM manually, by using a Settings app, provisioning packages, or the Company Portal app.

Automatic enrollment to MDM works for Windows devices, because only Windows devices can be joined to an on-premises AD DS and Microsoft Entra ID. Other devices, such as Android and iOS devices, can only be enrolled manually to MDM by using the Company Portal app. The Company Portal app isn't included on Android and iOS devices by default; it's available as a free app in Google Play store and the Apple app store. If you want to enroll iOS devices, you must ensure that MDM is configured with a valid Apple Push Notification (APN) certificate. iPhones, iPad, and macOS devices require an APN certificate for secure communication with MDM, regardless if MDM is Intune, MDM for Microsoft 365, or a third-party MDM product.

For more details, refer to [Enable Windows device automatic enrollment](https://learn.microsoft.com/en-us/mem/intune/enrollment/quickstart-enroll-windows-device).

#### Supported Devices

Intune supports various mobile devices and computers. Users can install the Company Portal app to help them enroll and remove devices, install published apps, and help them contact their IT support.

Intune supports devices running the following operating systems through device enrollment, which was discussed in the previous unit:

- Windows 10/11 (Home, Pro, Education, S mode, and Enterprise versions)
- Windows 10/11 Cloud PCs on Windows 365
- Windows 10 IoT and Windows 10 Holographic
- Windows 10 2019 LTSC
- Surface Hub
- Windows 10 Teams (Surface Hub)
- Apple iOS/iPadOS 14.0 and later
- macOS 11.0 and later
- Android 8.0 and later, including Samsung KNOX Standard 3.0 and higher
- Linux Ubuntu Desktop (20.04 or 22.04 LTS on x86/64)
- Chrome OS

 Note

Intune offered a software client for legacy operating systems. This is not needed on current supported operating systems.

#### Define Allowed Devices

By default, all users who are assigned an Intune license are allowed to enroll their supported device types to Intune. However, you can configure enrollment restrictions that users must meet before they can enroll a device. Enrollment restrictions can include the following criteria:

- Maximum number of devices that a user can enroll. By default, this is set to five devices per user.
    
- Device platforms that can be enrolled:
    
- Required operating system version for iOS, Android, Android work profile, and Windows devices
    
    - Minimum version
    - Maximum version
- Restrict enrollment of personally owned devices. You can configure this restriction for iOS, Android, Android work profile, macOS, and personally owned devices for Windows 10/11.
    

![Screenshot of the Configure platforms screen.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/configure-platform-326ebf7a.png)

You can manage device enrollment by configuring the following enrollment options:

- **Terms and conditions**. You can require that users accept the company's terms and conditions before they can use the Company Portal to enroll their devices and access resources such as company apps and email.
- **Enrollment restrictions**. You can configure device types that can be enrolled, block enrollment of personal devices, and restrict the number of devices that each user can enroll.
- **Enable Apple device enrollment**. You can control whether Apple devices can be enrolled; they can be enrolled only if you added an APN certificate to MDM.
- **Corporate identifiers**. You can list international mobile equipment identifier (IMEI) numbers and serial numbers to identify company-owned devices. Intune can perform additional management tasks and collect additional information such as the full phone number and an inventory of apps from company-owned devices. You can also prevent enrollment of devices that aren't company-owned.
- **Multifactor authentication**. When users enroll a device, you can require an additional verification method, such as a phone, PIN, or biometric data.
- **Device enrollment manager**. Device enrollment manager (DEM) can enroll large numbers of devices. A restriction on the number of devices that a user can enroll doesn't apply to DEM; DEM can enroll up to 1,000 devices.

#### Ensure Users Enroll Their Devices

To ensure that users enroll their devices, you can configure a Security policy in Microsoft 365 or a Conditional access policy in Intune to allow access to company resources only from enrolled devices. If such policy is in place and a user tries to access company resources, such as his or her Exchange Online mailbox, the user will be denied access and redirected to enroll his or her device first. After the user enrolls the device, he or she'll be able to access the mailbox.

Users can use their devices for personal work and leisure as soon as they obtain the device. But organizations don’t have control over such devices, and they can't manage them until the devices are enrolled to an MDM solution, such as Intune or MDM for Microsoft 365. However, because device enrollment is usually a manual process and users often forget to perform it, most organizations have resorted to making enrollment mandatory.

They only allow users to access company resources from enrolled devices that comply with organizational policy. They use compliance policies to define how devices should be configured and conditional access policies for controlling access to organizational resources. If a user tries to access resources from a non-enrolled device, he or she's denied access and asked to enroll the device first.

You can configure automatic enrollment to MDM for Windows devices only. If a Windows device is already joined to on-premises AD DS which is synced to Microsoft Entra ID, you can configure the **Enable automatic MDM enrollment using default Microsoft Entra credentials** Group Policy setting to enroll devices to MDM.

# Manage corporate enrollment policy

Completed100 XP

- 3 minutes

When your organization signs up for a Microsoft cloud-based service like Intune, you're given an initial domain name hosted in Microsoft Entra ID that follows this model: **your-domain.onmicrosoft.com**. In this example, **your-domain** is the domain name that you chose when you signed up. **onmicrosoft.com** is the suffix assigned to the accounts you add to your subscription. You can configure your organization's custom domain to access Intune instead of the domain name provided with your subscription.

Before you create user accounts or synchronize your on-premises Active Directory, we strongly recommend that you add one or more of your custom domain names. This will simplify user management and lets users sign in with the credentials they use to access other domain resources.

You can decide to use only the **.onmicrosoft.com** domain if you want to, but it should only be used for the initial setup or when you're testing. You can't rename or remove the initial **onmicrosoft.com** domain name. You can add, verify or remove custom domain names used with Intune to keep your business identity clear.

#### To add and verify your custom domain

1. Go to the Microsoft 365 admin center and sign into your administrator account.
    
2. In the navigation pane, choose **Setup** - **Domains**.
    
3. Choose **Add domain**, and type your custom domain name. Select **Next**.
    
    ![Screenshot of the 'Add a domain' screen, within the Microsoft 365 admin center.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/microsoft-365-admin-center-add-domain-7e79fc63.png)
    
4. The **Verify domain** dialog box opens giving you the values to create the TXT record in your DNS hosting provider.
    
    - GoDaddy users: Microsoft 365 admin center redirects you to GoDaddy's login page. After you enter your credentials and accept the domain change permission agreement, the TXT record is created automatically. Alternatively, you can create the TXT record.
    - Register.com users: Follow the step-by-step instructions to create the TXT record.

Once you've set up Intune, users enroll Windows devices by signing in with their work or school account.

As an Intune admin, you can simplify enrollment in the following ways:

- Enable automatic enrollment (Microsoft Entra ID P1 or P2 required)
- CNAME registration
- Enable bulk enrollment (Microsoft Entra ID P1 or P2 and Windows Configuration Designer required)

#### Configure automatic MDM enrollment

Automatic enrollment lets users enroll their Windows devices in Intune. To enroll, users add their work account to their personally owned devices or join corporate-owned devices to Microsoft Entra ID. In the background, the device registers and joins Microsoft Entra ID. Once registered, the device is managed with Intune.

1. Sign in to Microsoft Intune admin center located at [https://intune.microsoft.com](https://intune.microsoft.com/).
    
2. Select **Devices** - **Enroll devices** - **Automatic enrollment**.
    
3. Configure the MDM User scope. Specify which users’ devices should be managed by Microsoft Intune. These Windows devices can automatically enroll in Microsoft Intune.
    
    - **None** - MDM automatic enrollment is disabled
    - **Some** - Select the Groups that can automatically enroll their Windows devices
    - **All** - All users can automatically enroll their Windows devices
4. Use the default values for the following URLs:
    
    - MDM Terms of use URL
    - MDM Discovery URL
    - MDM Compliance URL
5. Select **Save**.
    

#### Simplify Manual Enrollment (Optional)

If you don't have Microsoft Entra ID P1 or P2, you can create a domain name server (DNS) alias (CNAME record type) that redirects enrollment requests to Intune servers. While optional, if no CNAME record is found, users are prompted to manually enter the MDM server name, enrollment.manage.microsoft.com.

##### Step 1: Create CNAME records

Create CNAME DNS resource records for your company’s domain. For example, if your company’s website is contoso.com, you would create a CNAME in DNS that redirects EnterpriseEnrollment.contoso.com to enterpriseenrollment-s.manage.microsoft.com.

Microsoft Entra ID has a different CNAME that it uses for device registration for iOS, Android, and Windows devices. If you plan to use conditional access, you should also configure the EnterpriseRegistration CNAME for each company name you have.

We recommend that you create both CNAME records for all DNS names that you own.

Expand table

|Type|Host name|Points to|TTL (Time-To-Live)|
|---|---|---|---|
|CNAME|EnterpriseEnrollment.contoso.com|EnterpriseEnrollment-s.manage.microsoft.com|1 hour|
|CNAME|EnterpriseRegistration.contoso.com|EnterpriseRegistration.windows.net|1 hour|

If the company uses more than one UPN suffix, you need to create two CNAME records for each domain name and point each one to EnterpriseEnrollment-s.manage.microsoft.com and EnterpriseRegistration.windows.net respectively.

##### Step 2: Verify CNAME

1. Sign in to Microsoft Intune admin center located at [https://intune.microsoft.com](https://intune.microsoft.com/).
2. In the left navigation, select **Devices** then select **Enroll devices**.
3. On the Windows enrollment page, select **CNAME Validation**.
4. In the **Domain** box, enter the company website and then select **Test**.

Changes to DNS records might take up to 72 hours to propagate. You can't verify the DNS change in Intune until the DNS record propagates.



# Enroll Windows devices in Intune

Completed100 XP

- 7 minutes

Enrolling personal and organization-owned devices in Intune can significantly enhance your organization's security and device management capabilities. Enrolling a device establishes a connection between the device and Intune, allowing you to manage and control the device remotely.

Once enrolled, the device will receive the policies and profiles you created, including email, Wi-Fi, security settings, and more configurations. These policies and profiles can be customized to meet your organization's specific needs, ensuring that your devices are configured and secured in accordance with your policies.

Enrolling personal devices in Intune can be particularly useful for organizations allowing employees to use their own devices for work purposes. With Intune, you can ensure that these devices are configured and secured properly without taking full control of the device or accessing personal data. This helps to maintain a balance between work and personal use of the device. Overall, enrolling personal and organization-owned devices in Intune is a powerful tool for device management and security, allowing organizations to maintain control over their devices and protect their data.

#### Enrolling Windows devices

Enrolling Windows devices into Microsoft Intune for device management has many ways. Some are user-driven, and IT administrators control some. Some exist to support BYOD programs, and others to streamline modern provisioning scenarios and management for corporate-owned devices. Each enrollment method can have different setup requirements and behaviors. The following methods can be utilized to complete Intune enrollment:

- Method 1: Add work or school account
- Method 2: Enroll in MDM only (user driven)
- Method 3: Microsoft Entra join (OOBE)
- Method 4: Microsoft Entra join (Autopilot – user-driven deployment mode)
- Method 5: Microsoft Entra join (Autopilot self-deploying mode)
- Method 6: Enroll in MDM only (Device Enrollment Manager)
- Method 7: Configuration Manager co-management
- Method 8: Microsoft Entra join (bulk enrollment)

##### Method 1: Add work or school account

This enrollment method will "Microsoft Entra join" the device. If you have Microsoft Entra ID P1 or P2 licenses and your Microsoft Entra tenant has auto-enrollment for Intune configured, your device will also be enrolled into Intune during this process. This method is preferred when Autopilot isn’t used in the environment. You would provide users with instructions on accessing the **“set up a work or school account”** from the **Settings** app.

![Screenshot of the Setup a work or school account window, which appears after selecting Connect from the Access work or school page.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/windows-add-work-school-account-40b25f77.png)

##### Method 2: Enroll only in device management (user driven)

This enrollment method will only enroll the device in Intune and not Microsoft Entra join the device. You’ll only use this form of enrollment in environments that don’t have Microsoft Entra ID P1 or P2 licenses required to enable auto-enrollment of devices into Intune.

![Screenshot of the Setup a work or school account window, which appears after selecting the Enroll only in device management option from the Access work or school page in Intune.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/windows-enroll-sign-work-school-dda8cbb6.png)

##### Method 3: Microsoft Entra join (OOBE)

This enrollment method does the same as method 1, with one exception. The device is enrolled during the Out of Box Experience (OOBE) and not from the **Settings** app. The device will be Microsoft Entra joined by choosing **Setup for an organization** and using a **Work Account** to sign in. If you have Microsoft Entra ID P1 or P2 licenses and your Microsoft Entra tenant has auto-enrollment for Intune configured, your device will also be enrolled into Intune. This method will be used when you need direct access to your users and their devices. This could be a remote office where the devices are delivered directly with Windows pre-installed, typically Windows Pro edition. The user then powers on the machine and joins Microsoft Entra ID during OOBE. The device is enrolled in Intune and will receive apps and configuration from Intune. The version of Windows is typically uplifted to Windows Enterprise edition using an Intune profile setting.

![Screenshot of the Sign in with Microsoft - work or school account page.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/windows-work-school-account-sign-86470f16.png)

##### Method 4: Microsoft Entra join (Autopilot – user-driven deployment mode)

This enrollment method does the same as method 2, with a few exceptions. The device is enrolled during the Out of Box Experience (OOBE), which is customized and not from the Settings app. Many of the OOBE screens can be skipped to ensure a smoother setup experience for end users. If configured, the desktop will first be shown to the user when installed software and policies are applied.

This method is preferred for enrolling devices in Intune, but it requires Microsoft Entra ID P1 or P2 licenses, and your Microsoft Entra tenant has auto-enrollment for Intune configured.

![Screenshot of sample sign-in screen. The title reads, Welcome to A. Datum Azure AD.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/windows-sign-azure-active-directory-d70a89a4.png)

##### Method 5: Microsoft Entra join (Autopilot self-deploying mode)

This enrollment method basically does the same as method 4, with one exception. It allows all OOBE screens to be skipped after the device is first powered on. The Microsoft Entra join and Intune enrollment are fully automated with no user interaction.

This type of enrollment is primarily for user-less devices such as kiosks, but it can also be used for normal users. You can pre-assign a user to a device so all the user has to supply is a password. This setup experience is the most streamlined compared to the other methods.

![Screenshot of the Autopilot profile settings page in Intune.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/intune-policy-set-region-1e566302.png)

##### Method 6: Enroll in MDM only (Device Enrollment Manager)

This method of enrollment is like method 3, except it’s performed by IT admins using a special type of account - A Device Enrollment Manager (DEM) account. The devices are enrolled and prepared by users before handing them out. The DEM would enroll the device, log on to the company portal and install the apps required by the user. This account can enroll up to 1000 devices into Intune. The IT administrator who performs the enrollment must have access to local administrator credentials to complete the enrollment from the Settings menu. For more information about DEM, refer to the topic **Enrollment Rules** later in this Module.

![Screenshot of the Device enrollment - Device enrollment managers screen.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/intune-device-enrollment-manager-add-0caa052a.png)

##### Method 7: Configuration Manager co-management

Co-management enables you to manage Windows devices concurrently by using both Configuration Manager and Intune. It’s a solution that bridges traditional to modern management and gives you a path to transition using a phased approach. Co-management is the preferred way to enroll existing devices, Microsoft Configuration Manager is already managing that. Once enabled, the device can be managed by Configuration Manager and Intune, using the best features of both.

##### Method 8: Microsoft Entra join (bulk enrollment)

Bulk enrollment is an efficient way to set up many devices to be managed by Intune without the need to re-image the devices. You enable bulk enrollment by creating a provisioning package using the Windows Configuration Designer app from the Store. You then apply this package during the OOBE or run it from the Settings app. If you want to make the enrollment process as easy as possible for your users, you can use this method instead of method 1. You don’t have to give users instructions on how to **set up a work or school** account from the **Settings** app. You provide them with the provisioning package, and all they need to do is select it to enroll in Microsoft Entra ID and Intune.

![Screenshot of the Windows Configuration Designer start page.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/windows-configuration-designer-create-menu-15ea5078.png)




# Enroll Android devices in Intune

Completed100 XP

- 3 minutes

You can let users enroll their personal devices for Intune management (BYOD). Once you've completed the prerequisites and assigned users licenses, they can download the Intune Company Portal app from the Google Play Store, and follow enrollment instructions in the app.

To enroll an Android device using the Company Portal, perform the following steps:

1. Install the free Intune Company Portal app from Google Play.
2. Open the Company Portal app.
3. On the Company Portal Welcome screen, tap **Sign in**, and then sign in with your work or school account.
4. Follow the instructions given in the Company Portal. The end-user experience can vary based on the policies assigned to the user and/or device.

#### Android Enterprise

Android Enterprise management makes it easier to define the scope of management for a particular device. This is helpful in balancing what information is managed by IT and what is managed by the device user or owner.

**Android Enterprise work profile**. Intune helps you deploy apps and settings to Android work profile devices to ensure work and personal information are separate. After enrollment, management capabilities only affect the work profile that is created on the device during enrollment. Users can install any app they choose to the personal side of the device. Administrators can manage and monitor apps and actions scoped to the work profile. Note that Android work profiles are supported on only certain Android devices.

- **Android Enterprise dedicated.** For corporate-owned, single use devices, such as digital signage, ticket printing, or inventory management. Admins lock down the usage of a device for a limited set of apps and web links. It also prevents users from adding other apps or taking other actions on the device.
- **Android Enterprise fully managed.** For corporate-owned, single user devices used exclusively for work and not personal use. Admins can manage the entire device and enforce policy controls unavailable to work profiles.

To set up Android Enterprise, you must connect your Intune tenant account to your Managed Google Play account and set up an enrollment profile based on what method of management is being used.

For more information, refer to [Enroll Android devices](https://learn.microsoft.com/en-us/mem/intune/enrollment/android-kiosk-enroll).


# Enroll iOS devices in Intune

Completed100 XP

- 8 minutes

You can let users enroll their personal devices for Intune management (BYOD). Once you've completed the prerequisites and assigned users licenses, they can download the Intune Company Portal app from the App Store, and follow enrollment instructions in the app.

Enroll your iOS device using Company Portal

1. Download and install the Intune Company Portal from Apple app store.
2. Open the Company Portal app.
3. On the Company Portal Welcome screen, tap **Sign in**, and then sign in with your work or school account.
4. Follow the instructions given in the Company Portal. The end-user experience can vary based on the policies assigned to the user and/or device.

#### Company-owned iOS devices

For organizations that buy devices for their users, Intune supports the following iOS company-owned device enrollment methods:

- Apple Business Manager (ABM)
- Apple’s Automated Device Enrollment (ADE)
- Apple School Manager
- Apple Configurator
- Intune Device Enrollment Manager (DEM) account
- **Device Enrollment Program**. Organizations can purchase iOS devices through Apple's Device Enrollment Program (DEP). DEP lets you deploy an enrollment profile “over the air” to bring devices into management.

The Apple Device Enrollment Program (DEP) is an online service that automates the enrollment and configuration of Apple iOS devices to MDM. Apple DEP is only available for devices that an organization purchases through either Apple or authorized resellers to provide to employees.

To enable DEP enrollment, you use both the Intune and Apple DEP portals. A list of serial numbers or a purchase order number is required so you can assign devices to Intune for management. On the Apple DEP website, an administrator can preconfigure device settings, including what applications and company services each device can access, and set devices to automatically enroll to MDM. iOS devices enrolled in DEP don't require manual configuration, and users never have to select on MDM links or install the Company Portal app to enroll the device.

If an organization allows its users to bring their own devices, the users should perform the regular iOS enrollment. But if the company provides employees with iOS devices that are part of the Device Enrollment Program, users can enroll those devices to MDM by performing following steps:

1. Turn on your iOS device.
    
2. After you select your **Language**, connect your device to Wi-Fi.
    
3. On the **Set up iOS device** screen, choose whether you want to:
    
    - Set up as new device
    - Restore from iCloud backup
    - Restore from iTunes backup
4. Once you’ve connected to Wi-Fi, the **Configuration** screen will appear. This will say:
    
    - [Your Company] will automatically configure your device.
    - Configuration allows [Your Company] to manage this device over the air. An administrator can help you set up email and network accounts, install and configure apps, and manage settings remotely. An administrator may disable features, install and remove apps, monitor and restrict your Internet traffic and remotely erase this device.
    - Configuration is provided by: [Your Company's] iOS Team [Address]
5. **Log in with your Apple ID**. Logging in lets you install the Company Portal app and install the management profile that will let your company give you access to its resources, such as email and apps.
    
6. Agree to the **Terms and Conditions** and decide whether you want to send diagnostic information to Apple.
    
7. Once you complete your enrollment, your device may prompt you to take more actions. Some of these steps might be entering your password for email access or setting up a passcode.
    

You can enable DEP enrollment for large numbers of devices without ever touching them. You can ship devices like iPhones and iPads directly to users. When the user turns on the device, Setup Assistant runs with preconfigured settings and the device enrolls into management.

For more information, refer to [Automatically enroll iOS devices with Apple's Device Enrollment Program](https://learn.microsoft.com/en-us/mem/intune/enrollment/tutorial-use-device-enrollment-program-enroll-ios).

#### Supervised mode

An iOS device in supervised mode can be managed with more controls. As such, it’s especially useful for corporate-owned devices. Intune supports configuring devices for supervised mode as part the DEP. We recommend that you use supervised mode even though it requires more configuration compared to other iOS enrollment methods. It gives you access to many policy settings in Intune that are otherwise unavailable.

Note that with iOS11 and later, supervised mode should always be enabled, as support for unsupervised mode in IOS11 was deprecated.


# Explore device enrollment manager

Completed100 XP

- 4 minutes

Organizations can use Intune to manage large numbers of mobile devices with a single user account. The device enrollment manager (DEM) account is a special user account that can enroll up to 1,000 devices. Organizations can use Intune to manage large numbers of mobile devices with a single user account. You add existing users to the DEM account to give them the special DEM options. Each enrolled device uses a single license. A DEM account is useful for scenarios where devices are enrolled and prepared before handing them out to the users of the devices. The DEM would enroll the device, log on to the company portal and install the apps required by the user. If the user requires individual configuration such as e-mail profiles, then the user should enroll the device themselves, and DEM shouldn't be used.

Users must exist in the Azure portal to be added as device enrollment managers. For optimal security, the DEM user shouldn't also be an Intune admin. The DEM enrollment method can't be used with these other enrollment methods: Apple Configurator with Setup Assistant, Apple Configurator with direct enrollment, Apple School Manager (ASM), or Device Enrollment Program (DEP).

### Example of a device enrollment manager scenario

A restaurant wants to provide 50 point-of-sale tablets for its wait staff, and order monitors for its kitchen staff. The employees never need to access company data or sign in as users. The Intune admin creates a new device enrollment manager account for the restaurant supervisor. This account is separate from the supervisor's primary account and is used only for enrolling shared devices with Intune. The supervisor can now enroll the 50 tablets devices by using the DEM credentials.

### What can a device enrollment manager do?

Only users in Microsoft Entra ID can be added as a device enrollment manager.

The DEM user can:

- Enroll up to 1000 devices in Intune
- Sign in to the Company Portal to get company apps
- Configure access to company data by deploying role-specific apps to the tablets

### Limitations of devices that are enrolled with a DEM account

Devices that are enrolled with a device enrollment manager account have the following limitations:

- No per-user access. Because devices don't have an assigned user, the device has no email or company data access. VPN configurations, for example, could still be used to provide device apps with access to data.
- The DEM user can't unenroll DEM-enrolled devices on the device itself by using the Company Portal. The Intune admin can unenroll.
- Only the local device appears in the Company Portal app or website.
- Users can’t use Apple Volume Purchase Program (VPP) apps with user licenses because of per-user Apple ID requirements for app management.
- (iOS only) If you use DEM to enroll iOS devices, you can't use the Apple Configurator, Apple Device Enrollment Program (DEP), or Apple School Manager (ASM) to enroll devices. This means that you can't put the device in supervised mode and thus won't have access to some configuration options.
- (Android only) There's a limit to the number of Android work profile devices that can be enrolled with a single DEM account. Up to 10 Android work profile devices may be enrolled per DEM account. This limitation doesn't apply to legacy Android enrollment.
- Devices can install VPP apps if they have device licenses.
- An Intune device license isn't required to use DEM.

### Add a device enrollment manager

1. Sign in to **Microsoft Intune admin center** located at [https://intune.microsoft.com](https://intune.microsoft.com/).
2. In the left navigation, select **Devices** - **Enroll devices** - **Device enrollment managers**.
3. Select **Add**. On the **Add User** panel, enter a user principal name for the DEM user, and select **Add**. The DEM user is added to the list of DEM users.

### Permissions for DEM

Global or Intune Service Administrator Microsoft Entra roles are required to:

- Complete tasks that are related to DEM enrollment in the Admin Portal
- Access all DEM users despite role-based access control (RBAC) permissions being listed and available under the custom User role

A user without the Global Administrator or Intune Service Administrator role assigned, but who has read permissions for the Device Enrollment Managers role, can access only the DEM users they created.


# Monitor device enrollment

Completed100 XP

- 3 minutes

As an Intune administrator, you must ensure that managed devices are providing the resources that your users need to do their work, while protecting that data from risk.

The Devices workload gives you insights into the devices you manage, and lets you perform remote tasks on those devices.

#### Monitoring enrolled devices

1. Sign in to the **Microsoft Intune admin center**.
    
2. Select **Devices**. This view shows detailed information about the individual devices, and what you can do with them, including:
    
    - **Overview** shows a visual snapshot of the enrolled devices, and also shows how many devices are using the different platforms, including Android, iOS, and more.
        
        ![Screenshot of the Devices, Overview screen.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/endpoint-manage-admin-center-devices-overview-7cec0bde.png)
        
    - **All devices** shows a list of the enrolled devices you manage.
        
        ![Screenshot of the Devices, All devices screen.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/endpoint-manage-admin-center-all-devices-f210129c.png)
        
        - Use the Export feature to create a .csv list of all the devices, in increments of 10,000 (Internet Explorer) or 30,000 (Microsoft Edge, Chrome).
        - Select any device to view additional details about that device, including hardware details, installed apps, its compliance policy status, and more.
    - **Monitor** provides several reports related to the status of devices.
        
        ![Screenshot of the Devices, Monitor Overview, Enrollment failures screen.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/intune-monitor-enrollment-failures-0d6af6b0.png)
        
        - Enrollment failures. Provides views of devices, which include the type of failure and method of enrollment.
        - Incomplete user enrollments. Using this information, you can update your onboarding documents to help users complete enrollment. For example, if many users are quitting at the Terms of Use, you might investigate that area and make it more intuitive for users.

#### Monitoring Microsoft Entra joined devices

Not all devices will be necessarily listed in the Microsoft Intune admin center, only devices that are enrolled in Intune. For devices that are joined to the domain, but haven't been enrolled in Intune, you can view these devices in the Azure portal.

1. Sign in to the Azure portal.
    
2. Select **Microsoft Entra ID**, and then select **Devices**.
    
    - **All Devices** shows a list of the devices registered or joined with Microsoft Entra ID.
        
        ![Screenshot of the Microsoft Entra Devices, All devices screen.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/azure-active-directory-devices-4b76d514.png)
        
    - **Device Settings** includes settings which users can join devices to Microsoft Entra ID, local administrator accounts, allowing users to register personal devices, and whether to require MFA.
        
    - **Enterprise State Roaming** defines which groups may sync settings and app data across devices.
        
    - **Audit Logs** log all activities that generated changes in Microsoft Intune. Audit logs include activities such as create, update, delete, and assign. You can review audit logs for most Intune workloads. Auditing is enabled by default, and it can't be disabled. As there can be many audit events, you can filter them based on several criteria or use Graph API to retrieve up to one year of audit events.
        
        ![Screenshot of the Monitor, Overview screen.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/intune-monitor-enrollment-failures-0d6af6b0.png)

The Devices feature provides additional details into the devices you manage, including their hardware and the apps installed. To view all your devices, and their properties do the following:

1. Sign in to the **Microsoft Intune admin center**.
2. Select **Devices** and then select **All Devices**. Select an individual device to view.

The **Overview** page is displayed by default. It shows the device name, and lists some key properties of the device, including whether it's a bring-your-own-device (BYOD) device, when it checked in, and more. The actions available depend on the device platform, and the configuration of the device.

- You can perform the following remote actions on the device:
    
    - **Retire**. Removes managed app data (where applicable), settings, and email profiles that were assigned by using Intune. The device is removed from Intune management
    - **Wipe**. Restores a device to its factory default settings. The user data is kept if you choose the **Retain enrollment state and user account** checkbox. Otherwise, all data, apps, and settings will be removed.
    - **Delete**. Remove devices from the Intune portal. The next time the device checks in, any company data on it will be removed.
    - **Remote lock (Android, iOS, macOS)**. Locks the device. To unlock the device, the device owner enters their passcode. Devices that don't have a PIN or password can't be remotely locked.
    - **Sync**. Forces the selected device to immediately check-in with Intune and immediately receives any pending actions or policies that have been assigned to it. This feature can help you immediately validate and troubleshoot policies you've assigned, without waiting for the next scheduled check-in.
    - **Reset passcode (iOs/Android)**. A device level reset of the passcode for the entire device.
    - **Restart**. Causes the device you choose to be restarted (within 5 minutes). The device owner isn't automatically notified of the restart, and they might lose work. Not supported for macOS or Android work profile devices.
    - **Fresh Start (Windows 10 and later only)**. Removes any apps that are installed on a PC. Fresh Start helps remove preinstalled (OEM) apps that are typically installed with a new PC.
    - **AutoPilot Reset (Windows 10 and later only)**. Initiates the reset process, avoiding the need for IT staff or other administrators to visit each machine to initiate the process.
    - **Quick scan (Windows 10 and later only)**. Performs a Microsoft Defender quick scan. Looks at common locations where there could be malware registered, such as registry keys and known Windows startup folders.
    - **Full scan (Windows 10 and later only)**. Performs a Microsoft Defender full scan.
    - **Update Microsoft Defender Security Intelligence**. Instructs the device to check for signature updates.
    - **BitLocker key rotation**. Remotely rotate the BitLocker recovery key of a device that runs version 1909 or later.
    - **Rename Device.** The Rename device action lets you rename a device that is enrolled in Intune. The device's name is changed in Intune and on the device.
    - **New Remote Assistance Session**. Devices managed by Intune can be administered remotely using TeamViewer. TeamViewer is a third-party program that you purchase separately.
    - **Locate device (Windows 10 and later, iOS, Android Enterprise dedicated).** Identifies the location (or last known location of Android dedicated devices) of a device or initiates a sound alert to assist in finding devices that support this feature.

![Screenshot of the Devices - Microsoft Entra devices screen.](https://learn.microsoft.com/en-us/training/wwl-azure/enroll-devices-use-intune/media/endpoint-manage-admin-center-device-overview-c304c3a0.png)

On the device details page, you can also manage and monitor the following:

- Use **Properties** to assign a device category you create and change ownership of the device to a personal device, or a corporate device.
- **Hardware** includes many details about the device, including the device ID, the operating system and version, storage space, the model and manufacturer, conditional access settings, and more details.
- **Discovered apps** lists all the apps that Intune found installed on the device, and the app versions. You can also Export the app list into a .csv file.
- **Device compliance** lists all assigned compliance policies, and if the device is compliant or not compliant.
- **Device configuration** shows all device configuration policies assigned to the device, and if the policy succeeded or failed.

Intune collects an app list on corporate-owned devices. With personal devices, only organizational managed apps are checked. For Windows clients, modern apps are listed for corporate-owned devices. Intune collect information about Win32 apps if the Intune management extention is installed on the device. Depending on the carrier used by the devices, not all apps may be collected.