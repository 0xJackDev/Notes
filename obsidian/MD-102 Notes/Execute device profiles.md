


Microsoft Intune includes settings and features that you can enable or disable on different devices within your organization. These settings and features are managed using profiles. Some profile examples include:

- A Wi-Fi profile that gives different devices access to your corporate Wi-Fi.
- A VPN profile that gives different devices access to your VPN server within your corporate network.



#### Types of device profiles

The following are examples of some of the profiles available in Intune. The types of profiles available depend on which platform you're creating the configuration profile under:

- **Administrative Templates:** The administrative templates include hundreds of settings that control features in Microsoft Edge version 77 and later, Internet Explorer, Microsoft Office programs, remote desktop, OneDrive, passwords and PINs, and more. These settings allow group administrators to manage ADMX-backed group policies using the cloud.
- **Certificates:** Certificates configure trusted, Simple Certificate Enrollment Protocol (SCEP), and Public Key Cryptography Standards (PKCS) certificates that can be assigned to devices, and used to authenticate Wi-Fi, VPN, and email profiles.
- **Device features - iOS and macOS:** Device features control features on iOS and macOS devices, such as AirPrint, notifications, and shared device configurations.
- **Device restrictions:** Device restrictions control security, hardware, data sharing, and more settings on the devices. For example, create a device restriction profile that prevents iOS device users from using the device camera.
- **Edition upgrade and mode switch:** Windows edition upgrades automatically upgrade devices that run some versions of Windows to a newer edition.
- **Email**. The email settings profile creates, assigns, and monitors Exchange ActiveSync email settings on the devices. Email profiles help ensure consistency, reduce support calls, and let end-users access company email on their personal devices, without any required setup on their part.
- **Endpoint protection:** Endpoint protection settings for Windows configure BitLocker and Microsoft Defender settings for Windows devices.
- **Identity protection:** Identity protection controls the Windows Hello for Business experience on Windows 10 and Windows 10 Mobile devices. Configure these settings to make Windows Hello for Business available to users and devices, and to specify requirements for device PINs and gestures.
- **Kiosk:** The kiosk settings profile configures a device to run one app or run multiple apps. You can also customize other features on your kiosk, including a start menu and a web browser.
- **VPN:** VPN settings assign VPN profiles to users and devices in your organization, so they can easily and securely connect to the network. Virtual private networks (VPNs) give users secure remote access to your company network. Devices use a VPN connection profile to start a connection with your VPN server.
- **Wi-Fi:** Wi-Fi settings assign wireless network settings to users and devices. When you assign a Wi-Fi profile, users get access to your corporate Wi-Fi without having to configure it themselves.
- **Custom profile:** Custom settings include the ability to assign device settings that aren't built-into Intune. Custom profiles will be explained in detail in a later unit.


# Create device profiles

Completed100 XP

- 3 minutes

As noted in the previous unit, many device profile types exist. Each platform has its own list of profile types. The process for creating device profiles is similar for all profiles.

To create a Windows device profile:

1. In the Microsoft Intune admin center, select **Devices**, then select **Windows** platform, then select **Configuration Profiles**.
    
2. Select **Create Profile**.
    
3. Enter the following properties:
    
    - **Platform**: Choose which versions of Windows to include.
    - **Profile type**: Select the type you want to create.

![This screenshot shows the Configuration profiles screen after the Create Profile button is selected. The Windows 10 and later platform has been selected, and is now prompting for a profile, with several options listed- Listed options include Administrative templates, custom, delivery optimization, device firmware configuration, Device restrictions, Domain Join, Edition Upgrade and switch, etc.](https://learn.microsoft.com/en-us/training/wwl-azure/execute-device-profiles/media/intune-create-profile-ae036674.png)

4. Select **Create**.

Once you create the profile, you'll be prompted to configure the settings of the profile across several tabs.

- **Basics**. Define a name for the profile and a description
    
- **Configuration Settings**. The profile type you defined in step 3 will determine what options are here. For example, if you choose the Device Restrictions profile, you'll see several options such as which control panel options are available, Microsoft Edge configurations, or App Store restrictions. Choosing the WiFi profile will allow you to configure settings such as SSID and EAP settings.
    
- **Assignments**. The profile can be assigned to the following:
    
    - Selected Groups
    - All Users & All Devices
    - All Devices
    - All Users
    
    Intune device configuration profiles let you exclude groups from policy assignment. For example, you can assign a device profile to the All sales users group, but exclude any members of the Sales Managers group. When you exclude groups from an assignment, exclude only users, or only exclude device groups (not a mixture of groups), Intune doesn't consider any user-to-device relationship. Including user groups while excluding device groups might not create the results you expect. When mixed groups are used, or if there are other conflicts, inclusion takes precedence over exclusion. For example, you want to assign a device profile to all devices in your organization, except kiosk devices. You include the All Users group, but exclude the All Devices group. In this case, all your users and their devices get the policy, even if the user’s device is part of the All Devices group. Exclusion only looks at the direct members of the groups, and doesn't include devices that are associated with a user. However, devices that don't have a user don't get the policy. This occurs because those devices have no relationship to the All Users group. If you include All Devices, and exclude All Users, then all the devices receive the policy. In this scenario, the intent is to exclude devices that have an associated user from this policy. However, it doesn't exclude the devices because the exclusion only compares direct group members.
    
- **Applicability Rules**. These rules allow further restriction of the profile assignment or exclusion specific OS versions or editions.
    
- **Review + create**. As the end of the process, a summary of the profile settings will be displayed, with the option to create the profile.

# Create a custom device profile

Completed100 XP

- 3 minutes

Intune may not have all the built-in settings you need or want. In other situations, you may want to use a setting available in other device profiles. To add these settings, create a device profile, and configure the profile with custom device settings. If you're looking for a specific Windows setting, remember that the Windows device restriction profile contains many settings that are built into Intune, and don't require custom values. Furthermore, new functionality is added to Intune frequently so you should always check to see if the setting you need is available as a native Intune setting.

#### Create a custom profile for Windows 10 and later devices

Use the Microsoft Intune custom profile for Windows 10 and later to deploy Open Mobile Alliance Uniform Resource Identifier (OMA-URI) values. These settings are used to control features on devices. Windows makes many Configuration Service Provider (CSP) settings available, such as Policy CSP.

1. In the Microsoft Intune admin center, select **Devices** > **Configuration profiles** > **Create profile** > **Windows 10 and later** as the platform. The Create profile pane opens with the Basics tab selected.
2. On the Configuration tab, in Custom OMA-URI Settings, select **Add** to create a new setting. You can also select **Export** to create a list of all the values you configured in a comma-separated values (.csv) file.
3. For each OMA-URI setting you want to add, enter the following information:
    - **Name**: Enter a unique name for the OMA-URI setting to help you identify it in the list of settings.
    - **Description**: Optionally, enter a description for the setting.
    - **OMA-URI** (case sensitive): Enter the OMA-URI for which you want to supply a setting.
    - **Data type**: Choose from:
        - String
        - String (XML)
        - Date and time
        - Integer
        - Floating point
        - Boolean
        - Base64
    - **Value**: Enter the value or file to associate with the OMA-URI you entered.
4. When you're done, select **OK**. In Create profile, select **Create**. The profile is created, and is shown in the profiles list.

#### Example

In the following example for Windows, the **Connectivity/AllowVPNOverCellular** setting is enabled. This setting allows a Windows device to open a VPN connection when on a cellular network.

![Screenshot of the create profile screen, with Settings tab selected and Custom OMA-URI Settings window shown.](https://learn.microsoft.com/en-us/training/wwl-azure/execute-device-profiles/media/custom-profile-1c31fa8a.png)

Not all settings are compatible with all Windows versions. The configuration service provider reference tells you which versions are supported for each CSP. Additionally, Intune doesn't support all the settings listed. To find out if Intune supports the setting you want, open the article for that setting. Each setting page shows its supported operation. To work with Intune, the setting must support the Add or Replace operations.

#### Create a custom profile for Android devices

Like Windows, Android Enterprise custom profiles use OMA-URI settings to control features on Android Enterprise devices. The steps for creating a custom Android profile are identical to creating a Windows custom profile, instead creating the profile under the Android platform.

Intune supports the following limited number of Android Enterprise custom profiles:

- Create a Wi-Fi profile with a pre-shared key: `./Vendor/MSFT/WiFi/Profile/SSID/Settings`
- Create a per-app VPN profile: `./Vendor/MSFT/VPN/Profile/Name/PackageList`
- Restrict copy and paste actions between work and personal apps on Android Enterprise devices: `./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste`

Only the settings listed can be configured by this profile type. Android devices don't expose a complete list of OMA-URI settings you can configure.

In addition to custom settings, you can use OEMConfig to add, create, and customize OEM-specific settings for Android Enterprise devices. OEMConfig is typically used to configure settings that aren't built in to Intune. Different original equipment manufacturers (OEM) include different settings. The available settings depend on what the OEM includes in their OEMConfig app.

#### Create a custom profile for Apple devices

Use the Microsoft Intune iOS/iPadOS or macOS custom profile to assign settings that you created by using the Apple Configurator tool to Apple devices. This tool lets you create many settings that control the operation of these devices and export them to a configuration profile. You can then import this configuration profile into an Intune iOS/iPadOS/macOS custom profile and assign the settings to users and devices in your organization.

This capability allows you to assign settings that aren't configurable with other Apple device profile types in Intune.

1. In the Microsoft Intune admin center, create a device profile for iOS/iPadOS or macOS as described in the previous unit, selecting **Custom** as the profile type.
    
2. On the Custom Configuration Profile pane, configure each of the following settings:
    
    - **Custom configuration profile name**: Provide a name for the policy as displayed on the device, and in Intune status.
    - **Configuration profile file**: Browse to the configuration profile that you created by using the Apple Configurator. Ensure that the settings you export from the Apple Configurator tool are compatible with the version of the OS on the devices to which you assign the custom policy. For information about how incompatible settings are resolved, search for Configuration Profile Reference and Mobile Device Management Protocol Reference on the Apple Developer website.
