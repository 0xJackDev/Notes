


This module will provide an overview of the different user profile types available for on-premises Windows devices. You’ll gain insights into the benefits of each type of profile and understand how to switch between them. You’ll explore how Folder Redirection functions and how to configure it. Finally, the module will conclude with an overview of Enterprise State Roaming and the steps involved in configuring it for Microsoft Entra devices.

### Objectives

Upon completion of this module, you should be able to:

- Explain the various user profile types that exist in Windows.
- Describe how a user profile works.
- Configure user profiles to conserve space
- Explain how to deploy and configure Folder Redirection.
- Explain what Enterprise State Roaming is.
- Configure Enterprise State Roaming for Microsoft Entra devices.

In Windows, a user profile contains a user state. A user profile is a set of files and folders. It's personal to each user who has signed in to the computer, and it’s stored in the Users folder. Windows requires each user who signs in to have a user profile. The Windows operating system creates a user profile when a user signs in for the first time. The initial user profile is based on the default user profile and is used for all subsequent sign-ins. User profiles contain details about the user environment, such as Start menu settings, desktop settings, user documents, and the user hive of the registry. By default, a user profile is located on the same drive as the Windows operating system in the C:\Users folder. The user profile is only applicable when a user logs in to the same device, but you can alter the user profile type if you wish to use it for multiple computers.

User profiles provide the following advantages:

- When the user logs on to a computer, the system uses the same settings that were in use when the user last logged off.
- When sharing a computer with other users, each user receives their customized desktop after logging on.
- Settings in the user profile are unique to each user. The settings can't be accessed by other users. Changes made to one user's profile don't affect other users or other users' profiles.

#### Elements in a user profile

User state consists of four main data categories, including:

Expand table

|**Category**|**Description**|
|---|---|
|User settings|This component describes all settings that a user has personalized after the operating system was installed.|
|User registry|This is the part of a computer’s registry that is specific to each user. Registry hive HKEY_CURRENT_USER (HKCU) stores settings that are specific to the currently signed-in user. The HKCU registry key is a link to the HKEY_USERS subkey that corresponds to the user. The same information is accessible in both locations. On computers that run Windows, each user's settings are stored in their own files, named NTUSER.DAT. These files are in the Users folder on the boot volume. Settings in the HKCU hive follow users with a roaming profile from device to device.|
|Application Data|The AppData folder, short for Application Data, is part of user state. This folder contains mostly application settings that are specific to a user. For example, if a user installs Microsoft Word 2016 and personalizes settings to fit their needs, such as adjusting toolbars, proofing, or language settings, Word 2016 stores these settings in the AppData folder. All well-designed applications should store their data in the AppData folder. However, it’s not possible to enforce this, and it’s entirely up to the developer to decide where an application stores its data. AppData folder provides a high degree of separation for user-related and computer-related application settings.|
|User data|This component contains all user-specific data, such as files, which are stored in multiple user profile sub-folders, such as Documents, Favorites, Pictures, and Music. Users can change this location and store their data in any other folder to which they have Write permissions. However, by default, user data is stored in the individual user profile.|

When a user signs into a device for the first time, a new user profile is created. The configuration for that is based on the configuration of the Default Profile. A default profile is a pre-configured baseline profile, which contains all of the initial settings to be included, whenever a new profile is created.



# Explore user profile types

Completed100 XP

- 3 minutes

Windows has different types of user profiles for the various different scenarios in how user configurations might be applied. The four common different types of user profiles are:

- **Local User Profile:** This type is available on a single computer only.
- **Roaming User Profile:** This type can roam between computers that are domain members.
- **Mandatory User Profile:** This is a special type of pre-configured user profile that doesn't store user changes between sign-ins.
- **Temporary User Profiles:** A temporary profile is issued each time that an error condition prevents the user's profile from loading.

#### Local user profiles

When a user signs in for the first time, the Windows operating system automatically creates a local user profile for all subsequent sign-ins to the same computer. A local user profile is used only when a user signs in to the computer where the profile was created, and it’s useful when a user is using a single computer. If a user roams between multiple computers, then by default, separate local user profiles will be created on each computer. This means that modifications and documents that a user creates on one computer won't be available on other computers. Therefore, administrators should avoid local profiles if users sign in to multiple devices.

#### Roaming user profiles

In a domain environment, administrators can configure a user with a roaming user profile by configuring his or her profile path. With roaming user profiles, user settings and data are stored on a network location and locally on the computer where a user signs in. When a user signs in, the local copy of the user profile is compared to the copy that is stored on the network location, and only newer files are copied locally. The user can change settings and create data files, which are stored in the local user profile copy. These changes copy to the network location when the user signs out. If users roam between multiple computers, their documents and settings follow them. If a user profile contains a lot of data, or if a user stores large files on the desktop, then signing in to the computer might take a long time. If a user signs in to multiple computers at the same time, changes performed on one computer override changes performed on a second computer because user profile changes copy to the network location only when the user signs out. Some parts of a user profile, such as Temporary Internet Files or AppData\Local, never copy to the network location even if roaming user profiles are used. You should be aware that roaming user profiles are incompatible between different versions of Windows operating systems.

#### Mandatory user profiles

A mandatory user profile is a type of roaming user profile that administrators can configure. With mandatory user profiles, user changes are stored in the local copy of a user profile but aren't preserved after a user signs out from the computer. When the user signs in again, the mandatory user profile downloads from the network location, and it overrides the local user profile copy. The two types of mandatory user profiles are normal mandatory profiles and super-mandatory profiles. Administrators can configure users with mandatory user profiles first by configuring them with roaming user profiles and then by renaming the Ntuser.dat file in their profiles to Ntuser.man. The .man extension causes user modifications to the profile to be discarded at the next sign-in and user profiles to behave as read-only.

#### Temporary User Profiles

A temporary profile is issued each time that an error condition prevents the user's profile from loading. Temporary profiles are deleted at the end of each session, and changes made by the user to desktop settings and files are lost when the user logs off.

#### Profile extension for each Windows version

The name of the folder in which you store the profile must use the correct extension for the operating system it will be applied to. The following table lists the correct extension for each operating system version.

Expand table

|**Client operating system version**|**Server operating system version**|**Profile extension**|
|---|---|---|
|Windows 10, versions 1507 and 1511|N/A|V5|
|Windows 10, versions 1607, 1703, 1709, 1803, 1809, 1903 and 1909|Windows Server 2016 and Windows Server 2019|V6|

For example, if a profile is being creating for Windows v20H2, the path to the profile folder might be _\server\share\profile.v6_, with the extension indicating which version.



# Examine options for minimizing user profile size

Completed100 XP

- 3 minutes

Considering user profiles keep user state and users can modify their state, users must possess Write permissions to their user profiles. As long as users have Write permissions, they can write as much data as they want if there’s available free disk space unless an administrator limits them. Because user profiles contain user data, and user data can increase rapidly.

For example, if users store large graphic or multimedia files in their Documents folder, which is in their profile, an administrator often limits the space for storing user profiles.

Administrators can do this in several ways:

- Use quotas to limit the space that is available to a user on a volume or on a shared folder where the roaming user profile is stored.
- Redirect folders that typically contain large user files and are stored in the user profile by default, for example, the Documents folder, outside of the user profile.
- Use the Group Policy setting to limit user profile sizes. You can limit the size of local or roaming user profiles by configuring settings in the user part of Group Policy.

#### Use quotas

An option to limit user profile sizes is to use quotas. You can use the same approach to limit the disk space that a user consumes in general, and it applies to limiting user profile sizes. You can set a disk quota on a local Windows volume by using volume properties. By using File Server Resource Manager in Windows Server 2016, you can set a quota on a shared folder on the file server where roaming user profiles or redirected folders are stored. If you set a disk quota on a local volume, users won't be able to write more data when they reach their disk quota. If a quota is set on a shared folder, the local copy of a roaming user profile won't synchronize with the network share, and changes to the user profile won't copy to the file server until the user deletes some data and the local copy of the roaming user profile is smaller than the quota limit. In such cases, users will see a message during sign-out that their roaming user profiles didn't completely synchronize, and an entry will be added to Event Viewer.

#### Redirect folders out of user profiles

You can make user profiles smaller by redirecting folders that typically consume a large amount of storage space, out of the user profiles. When you do that, the redirected folders are available from any computer in AD DS even if the user is configured with a local user profile. You can configure Folder Redirection by using Group Policy, and several settings are available for each redirected folder. Even if you use Folder Redirection, you can also use quotas to limit the size of redirected folders.

#### Use Group Policy to limit user profile sizes

You can keep local and roaming user profile sizes in check by activating the Limit profile size setting in the user part of Group Policy. When you activate this, you can decide the max profile size and craft a unique message that users get when their profiles go over the limit. With local user profiles, users can be periodically reminded that their user profile exceeds the allowed size, but they can still write data to their profiles and sign out. Roaming user profiles means users can sign out, however, changes to their local copy won't sync up with the network. That means any changes to their local profile won't be copied to the file server until they delete some data and get the size of their local roaming user profile to be smaller than what's allowed in Group Policy.

Users can have smaller user profiles if they store data files outside of their user profiles, for example, in a dedicated shared folder or in the home folder.


Folder Redirection is a Group Policy setting that is most often used for configuring user profiles. Administrators can use Folder Redirection to redirect individual folders from a user profile to a new location. For example, an administrator can redirect the Documents folder from a local or roaming user profile to a separate network location. Redirected folder content is available from any computer on a network, and it doesn't copy to the computer on which a user signs in, as with roaming user profiles. Folder Redirection also provides users with access to the same data from multiple domain computers without copying data locally, as is the case with roaming user profiles. You can configure Folder Redirection by modifying Policies\Windows Settings\Folder Redirection settings in the User Configuration part of Group Policy.

Redirected folders are stored on a network share only, and users access them transparently in the same way as when they're stored in a local user profile. The Offline Files feature, which is enabled by default when redirected folders are used, provides users with access to content in redirected folders even without network connectivity.

Administrators configure Folder Redirection by using user settings in Group Policy, and by doing so, can redirect individual folders in a user profile. In Windows, an administrator can redirect 13 folders in user profiles, including Desktop, Start Menu, and Documents. Administrators can redirect predefined folders and folders in a user profile only. For each user with redirected folders, Windows creates a new sub-folder with the user’s sign-in name, and folders can be redirected to the same location or to a different location based on user group membership.

When you configure Folder Redirection, you can configure what happens if Folder Redirection is no longer effective. The options are to leave the redirected content on the network location or to move the content to the original location to a user’s profile. Folder Redirection can redirect many parts of a user profile, but settings that are stored in Ntuser.dat can't be redirected. Because of this, some administrators use roaming user profiles with Folder Redirection.

Folder Redirection provides several advantages:

- Redirected folder content is available from any computer in the domain.
- Redirected folder content doesn't copy to local computers, which minimizes network traffic during user sign-in.
- Administrators can set quotas (limiting disk space) and permissions on redirected folders. By doing so, administrators can control how much space a user can utilize and whether the user can modify contents of that part of the folder - for example, Desktop.
- Redirected folders are stored on network locations (network shares) and not on local computers. If a local hard drive fails, users can still access data in redirected folders from a different computer.
- Redirected folder content can be backed up centrally because it isn't stored locally on user computers. If Shadow Copies for Shared Folders is configured on a network location, users can access previous versions of their redirected files.

#### Overview of Folder Redirection deployment

The following steps give you an overview of how to configure and test Folder Redirection. These steps contain mock details for the purposes of demonstration. You can change the details to fit your organization’s environment.

1. On a client, verify that the location of the user’s **Desktop** folder is _C:\Users\username_.
2. Verify that the location of the user’s **Documents** folder is _C:\Users\username_.
3. Create a Group Policy that redirects the **Documents** folder for the user to a network folder.
4. Verify that the network folder is empty.
5. On the client, run **gpupdate /force**, and then sign out.
6. Sign in to the client as a user that will be affected by the Group Policy.
7. On the client, verify that the location of user’s Desktop folder is still _C:\Users\username_, as you didn't redirect it.
8. Verify that the location of user’s **Documents** folder is now redirected to the network folder.
9. In Notepad, create a file named **Demo Document** in which you type your name, and then save it in the **Documents** folder.
10. Verify that the network folder is no longer empty and that it has a sub-folder named username.
11. Sign in to another client as the same user.
12. On the other client, verify that the location of user’s **Desktop** folder is still _C:\Users\username_, as you didn't redirect it.
13. Verify that the location of the user’s **Documents** folder is the network folder.
14. View the content of the **Demo Document** file, and then verify that it has the same content that you typed on the first client.

For a detailed description on how to configure and deploy Folder Redirection, refer to Deploy Folder Redirection with Offline Files.


# Sync user state with Enterprise State Roaming

Completed100 XP

- 3 minutes

Windows offers advanced techniques for managing user profiles and data. By using cloud-based services such as Enterprise State Roaming and Microsoft OneDrive, companies can seamlessly empower their users to transition between various device platforms. With these services, employees can effortlessly access their data from any device and transfer their settings from one Windows device to another.

### Enterprise State Roaming

Windows 8 introduced the Sync your settings feature, which uses Microsoft accounts to sync settings with Microsoft OneDrive. Enterprise State Roaming offers similar functionality, but it's targeted to enterprises, because it requires Microsoft Entra ID P1 or P2 and it syncs Windows settings with Azure. Enterprise State Roaming can sync only settings and not data. However, you should note that Enterprise State Roaming can only sync the settings of the Universal Windows Platform (UWP) apps and Windows settings, and that it can't sync desktop-application settings. You can use the Settings app, Group Policy or mobile device management (MDM) to control which settings will be synced.

![Screenshot of two Windows 10 computers that are connected to Microsoft Entra ID P1 or P2 illustrating that Enterprise State Roaming can sync Windows 10.](https://learn.microsoft.com/en-us/training/wwl-azure/maintain-user-profiles/media/enterprise-sync-settings-c2bf2ecc.png)

Enterprise State Roaming syncs settings across Microsoft Entra joined devices and provides users with the same experience across their devices. Enterprise State Roaming provides the following benefits:

- Separation of business and private data. Business data and private data are stored separately. If a user installs an app by using a Microsoft Entra identity, the assumption is that the app is for business use. If an app was installed by using a Microsoft account, it's considered a personal app. Enterprise State Roaming syncs only state of the business UWP apps.
- Enhanced security. Synced data is automatically encrypted by using Azure Rights Management (Azure RMS) when it moves from a Windows device to the cloud and back. All data that is stored in the cloud is encrypted. When you enable Enterprise State Roaming, your company is automatically issued a free, limited-use license for Azure RMS. This free subscription is limited to encrypting and decrypting enterprise settings and application data synced by Enterprise State Roaming.
- Better management and monitoring. You can enable and configure Enterprise State Roaming in the Azure portal or by using Windows PowerShell. In the portal, you can view information such as which devices are synced by Enterprise State Roaming, who syncs data in your company, and when devices were last synced.
- Synced data is kept in the same region. Enterprise State Roaming data is hosted in the Azure region that best aligns with the Microsoft Entra tenant’s country/region, and data resides locally in the geographical region and doesn't replicate across regions.
- Data retention. Enterprise State Roaming data that was synced to Azure is kept at least 90 days after it was last accessed or until you delete it manually.

#### Sync user data

Enterprise State Roaming (ESR) doesn't provide a mechanism for synchronizing user files, such as documents and pictures. For this, OneDrive is a service that enables the ability to store and access files from all your devices, by storing data in the cloud. Together, OneDrive and ESR provide a modern method for providing users a seamless experience when using different devices. The modern method is fairly straight-forward. User data and settings are seamlessly synchronized between the client device and the cloud. When a user logs in to any other (approved) device, the user’s data and settings follow.

The primary advantage of using the modern method is that it's relatively easy to set up and doesn't require any customer infrastructure other than internet access. This greatly reduces the risks inherent with migrations and simplifies the migration process, since potentially no effort need be made to back up or transfer user data.

The disadvantage of this is that ESR and OneDrive don't provide a solution for synchronizing all the data in a user profile, most notably, application data associated with desktop apps. Depending on the applications the organization uses and how critical the app data is, will determine whether a modern or traditional method is needed. However, as client desktops are a single point of failure, organizations should strive to find solutions for moving critical data off of client devices.

#### ESR and Microsoft Edge (Chromium based)

ESR is a tool used to sync settings across the Windows ecosystem. With Microsoft Edge, the sync solution isn’t tied to Windows sync ecosystem. This enables us to offer Microsoft Edge across all the platforms, such as Windows 8.1, iOS, Android and macOS.

With Microsoft Edge sync, the following data will sync between devices:

- Favorites
- Passwords
- Form-fill
- History
- Open tabs (sessions)
- Settings (preferences)
- Extensions

 Note

Microsoft Edge doesn't use Windows credential Manager for passwords and as a result, won't sync passwords with Internet Explorer or other apps that use Windows Credential manager.

### User Experience Virtualization

User Experience Virtualization (UE-V) is a Windows Enterprise edition feature that enables the synchronization of operating-system settings, desktop-application settings, Microsoft Store app settings, network printers, and user credentials between Windows Enterprise edition computers in the same AD DS domain environment.

While UE-V is still a current product, it should be noted that UE-V is currently in extended support, scheduled to reach end-of-life on April 14, 2026.



# Configure Enterprise State Roaming in Azure

Completed100 XP

- 3 minutes

When you enable Enterprise State Roaming, your organization is automatically granted a free, limited-use license for Azure Rights Management protection from Azure Information Protection. This free subscription is limited to encrypting and decrypting enterprise settings and application data synced by Enterprise State Roaming. You must have a paid subscription to use the full capabilities of the Azure Rights Management service.

#### To enable Enterprise State Roaming

1. Sign in to the Azure portal.
2. Select **Microsoft Entra ID** > **Devices** > **Enterprise State Roaming**.
3. Select either **All** or **Selected** next to **Users may sync settings and app data across devices**. ![Screenshot of the Devices - Enterprise State Roaming screen.](https://learn.microsoft.com/en-us/training/wwl-azure/maintain-user-profiles/media/azure-enterprise-state-roaming-6ca7af98.png)

For a Windows device to use the Enterprise State Roaming service, the device must authenticate using a Microsoft Entra identity. For devices that are joined to Microsoft Entra ID, the user’s primary sign-in identity is their Microsoft Entra identity, so no additional configuration is required. The IT admin must Configure Microsoft Entra hybrid joined devices for devices that use on-premises Active Directory.

#### What data roams?

**Windows settings**: the PC settings that are built into the Windows operating system. Generally, these are settings that personalize your PC, and they include the following broad categories:

- Theme, which includes features such as desktop theme and taskbar settings.
- Internet Explorer settings, including recently opened tabs and favorites.
- Passwords, including Internet passwords, Wi-Fi profiles, and others.
- Language preferences, which include settings for keyboard layouts, system language, date and time, and more.
- Ease of access features, such as high-contrast theme, Narrator, and Magnifier.
- Other Windows settings, such as mouse settings.

**Application data**: Universal Windows apps can write settings data to a roaming folder, and any data written to this folder will automatically be synced. It’s up to the individual app developer to design an app to take advantage of this capability.

#### Data storage

Enterprise State Roaming data is hosted in one or more Azure regions that best align with the country/region value set in the Microsoft Entra instance. Enterprise State Roaming data is partitioned based on three major geographic regions: North America, EMEA, and APAC. Enterprise State Roaming data for the tenant is locally located with the geographical region and isn't replicated across regions.

The country/region value is set as part of the Microsoft Entra directory creation process and can't be subsequently modified.

#### View per-user device sync status

Follow these steps to view a per-user device sync status report.

1. Sign in to the Azure portal.
2. Select **Microsoft Entra ID** > **Users** > **All users**.
3. Select the user, and then select **Devices**.
4. Under **Show**, select **Devices syncing settings and app data** to show sync status.
5. If there are devices syncing for this user, you see the devices shown here.

#### Data retention

Data synced to the Microsoft cloud using Enterprise State Roaming is retained until it’s manually deleted or until the data in question is determined to be stale.

#### Explicit deletion

Explicit deletion is when an Azure admin deletes a user or a directory or otherwise requests explicitly that data is to be deleted.

- **User deletion**: When a user is deleted in Microsoft Entra ID, the user account roaming data is deleted after 90 to 180 days.
- **Directory deletion**: Deleting an entire directory in Microsoft Entra ID is an immediate operation. All the settings data associated with that directory is deleted after 90 to 180 days.
- **On request deletion**: If the Microsoft Entra admin wants to manually delete a specific user’s data or settings data, the admin can file a ticket with Azure support.

#### Stale data deletion

Data that hasn't been accessed for one year (“the retention period”) will be treated as stale and may be deleted from the Microsoft cloud. The retention period is subject to change but won't be less than 90 days. The stale data may be a specific set of Windows/application settings or all settings for a user. For example:

- If no devices access a particular settings collection (for example, an application is removed from the device, or a settings group such as “Theme” is disabled for all of a user’s devices), then that collection becomes stale after the retention period and may be deleted.
- If a user has turned off settings sync on all his/her devices, then none of the settings data will be accessed, and all the settings data for that user will become stale and may be deleted after the retention period.
- If the Microsoft Entra directory admin turns off Enterprise State Roaming for the entire directory, then all users in that directory will stop syncing settings, and all settings data for all users will become stale and may be deleted after the retention period.

#### Deleted data recovery

The data retention policy isn't configurable. Once the data is permanently deleted, it’s not recoverable. However, the settings data is deleted only from the Microsoft cloud, not from the end-user device. If any device later reconnects to the Enterprise State Roaming service, the settings are again synced and stored in the Microsoft cloud.