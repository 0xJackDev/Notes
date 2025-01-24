
Traditionally, the process of deploying a new device begins with wiping the device with whatever operating system was pre-installed and deploying one of the organization’s images to the device. However when admins are purchasing a device from an OEM (Original equipment manufacturer) , Windows 11 is already the OS on the device. While simply using the OEM image isn’t practical, Windows 10 introduced a new process called Windows Autopilot. Autopilot is designed to achieve the desired outcome of deploying a new hardware or refreshing an existing hardware with the organization’s desired configuration, without the process of creating, managing, and pushing large images over the network.

### Objectives 

After completing this module, you'll be able to:

- Explain the benefits of modern deployment for new devices.
- Describe the process of preparing for an Autopilot deployment.
- Describe the process of registering devices in Autopilot.
- Describe the different methods and scenarios of Autopilot deployments.
- Describe how to troubleshoot common Autopilot issues.
- Describe the process of deployment using traditional methods.




Modern deployment methods take a new approach to provisioning devices. One of the key benefits of Windows 10 and later is a feature called Windows Autopilot. Windows Autopilot is a cloud-based deployment method. With Autopilot, you can set up and preconfigure new and existing Windows 10 or later devices. Users in your organization use a new operating system out-of-the-box experience (OOBE) to configure their devices without needing a Windows image.

Autopilot offers the following advantages over on-premises deployment methods:

- You don't need to use images.
- You don't need to customize the deployments by injecting drivers.
- You don't need to deploy and maintain a deployment infrastructure.
- Configuring Autopilot deployments are relatively simple compared to traditional image creation and management.
- With no images to deploy, heavy bandwidth consumption is no longer a concern.

Windows Autopilot is cloud-driven and based around Azure AD Premium and Microsoft Intune. Using Windows Autopilot, you can:

- Join devices to Azure AD automatically.
- Auto enroll your users' devices into MDM services.
- Restrict the creation of the Administrator account.
- Customize the OOBE content specifically to your organization.

### New devices

Most organizations purchase new devices from an Original Equipment Manufacturer (OEM). In this process, they typically buy the device with an OEM license of Windows 11 (usually Pro edition). Organizations rarely desire the OEM image, and until Windows 10, they reimaged the device to configure it to organizational requirements.

It's no longer necessary to reimage the device when it already has Windows 11 or later. Regardless of the OEM image configuration or installed applications, Autopilot can reconfigure the device to suit the organization's requirements, including installing Line-Of-Business Apps and even changing the edition (such as switching from Pro to Enterprise).

From the user's standpoint, turning on the device initiates an Out-of-Box Experience (OOBE), during which the organization determines which options can be configured by the user. One potential benefit is the ability to have a zero-touch installation (ZTI) experience, meaning the device is ready to use simply by plugging it in and turning it on.

### Refresh existing devices

Over time, scenarios arise where it might be beneficial to refresh the device. Performance might be impacted as more apps are installed over time, and it can lead to intermittent issues or challenges that are not easily resolved. IT might elect to perform a wipe-and-load, and as with new deployments, Autopilot can be used instead of traditional methods. Similarly, if a device is reassigned to another user, Autopilot can be used to reset the device with a new OOBE as if the device was wiped and reimaged.

Windows 10 and later still supports traditional deployment. Many organizations use image-based deployment to upgrade their computers to Windows 11, although in-place upgrade is the recommended upgrade path when upgrading from Windows 8.1. Once a device is upgraded to Windows 11, organizations have the choice as to whether they continue to use image-based deployment or adopt modern deployment methods such as Autopilot or, in the case of upgrading from Windows 11, using Feature update.

### Autopilot compared to traditional methods

The following table compares traditional and modern Windows 11 deployment.

Expand table

|--|Traditional deployment|Modern deployment|
|---|---|---|
|Deploys Windows 11 images|Yes|No|
|Can be used with any preinstalled operating system|Yes|No|
|Requires a previous Windows 11 installation|No|Yes|
|Uses an on-premises infrastructure|Yes|No|
|Tools for preparing the deployment|Windows ADK, Windows Deployment Services, Microsoft Deployment Toolkit (MDT), and Configuration Manager|Windows Configuration Designer and Windows Autopilot|

There are certain circumstances where traditional installation methods must be used instead of Autopilot. These scenarios include:

- Bare-metal deployments.
- When the storage hardware where Windows 11 is installed must be replaced.
- In the event of a corrupted Windows 11 installation.
- When an organization requires prompts for custom user information beyond what the OOBE provides (such as customizing the LTI interface with MDT).



Basically Use windows Autopilot whenever setting up devices that already had windows 11 installed, but if there was no operating system or a old one before windows 10 Maybe do manual. Or if someone wants to use a image for some reason. Also Autopilot needs internet connectivity
Organizations must also be using Entra ID for Windows autopilot. As autopilot depends on Microsoft store for business or Intune and both require Entra ID. You will need Entra ID p1 or p2 to use autopilot






After you meet all the prerequisites, you can set up Windows Autopilot deployment. The setup process includes:

- Obtaining the hardware IDs of the devices that you want to deploy to the cloud service.
- Uploading the hardware IDs
- Creating a Windows Autopilot deployment profile.
- Applying the Windows Autopilot deployment profile to the devices or device groups.



### Manage Windows Autopilot in Intune

If you want to manage Windows Autopilot in the Intune, you must configure automatic mobile device management enrollment of Azure AD member Windows 11 devices. You can configure automatic mobile device management enrollment by performing the following steps:

1. In the Azure portal, select **Azure Active Directory**.
2. On the Azure Active Directory blade, select **Mobility (MDM and MAM)**, and then in the details pane, select **Microsoft Intune**.
3. On the Microsoft Intune blade, in MDM user scope, select **All** if you want all users to be able to enroll their devices to mobile device management. If you want only some users to be able to enroll their devices to mobile device management, select **Some**, specify the groups whose members should be able to enroll, and then select **Save**.

### Create a Windows Autopilot deployment profile

Once device IDs have been uploaded, a Windows Autopilot deployment profile must be created. This profile specifies the settings that should apply to the devices that you deploy by using Windows Autopilot. You can create and use multiple deployment profiles with Windows Autopilot, but you only use a single profile to deploy each device. Using Intune, you can use the following high-level procedure to create a deployment profile:

1. Sign in to Intune as a global admin, and in the portal, select **Device enrollment**, select **Windows enrollment**, select **Deployment Profiles** and then select **Create Profile**. Provide a Name and Description.
2. Then, for Deployment mode, choose between user-driven and self-deploying. With the former, the user specifies credentials during deployment, and devices with this profile are associated with the user account. With the latter, user credentials aren't required to enroll the device, and devices with this profile aren't associated with the user account.
3. Next, configure the Out-of-box experience (OOBE) settings, which include: language, keyboard, EULA, privacy settings, and user account.
4. Finally, create the profile. The Autopilot deployment profile is now available to assign to devices.

### Apply a deployment profile

Next, the deployment profile is applied to a device or a group of devices. Until you apply the deployment profile, Windows Autopilot doesn’t manage the OOBE setup phase on the device. After you apply the profile, Windows Autopilot takes control of the OOBE setup phase on the devices to which you apply the profile. You can use the following high-level process to apply the profile:

1. Sign in to Intune as a global admin, and in the portal, select **Device enrollment**, select **Windows enrollment**, select **Deployment profiles**, and then choose a profile.
2. Choose **Assignments**, and then select the group(s) that you want to assign the profile to.

After the setup process is complete, you can turn on the devices, and Windows Autopilot manages their OOBE setup phases.




### User-driven mode

Windows Autopilot user-driven mode is designed to enable new Windows 10 or later devices to be transformed from their initial state, directly from the factory, into a ready-to-use state without requiring that IT personnel ever touch the device. The process is designed to be simple so that anyone can complete it, enabling devices to be shipped or distributed to the end user directly with simple instructions:

- Unbox the device, plug it in, and turn it on.
- Choose a language, locale and keyboard.
- Connect it to a wireless or wired network with internet access.
- Specify your e-mail address and password for your organization account.

To enable User-driven mode for Azure Active Directory join, the following actions must be taken as part of preparing the Autopilot deployment:

- Users must be able to join Azure AD.
- If using Intune (and not Microsoft Store for Business), user-driven mode must be selected in the Autopilot profile assigned to the device if using Intune. The Autopilot profile must also be assigned to an Azure AD device group.
- The device must be added to Windows Autopilot and a profile must be assigned to the device.

User-driven mode is also supported for hybrid Azure Active Directory join. In addition to the actions above, the following steps must also be taken:




### Self-deploying mode

Windows Autopilot self-deploying mode enables a device to be deployed with little to no user interaction, achieving a ZTI experience with all OOBE prompts pre-configured. The enrollment status page will display while the device is being configured, and then the computer will either complete and display the sign-in screen, ready for Azure AD credentials. If the device is configured as a kiosk device, it will automatically sign in by using a locally configured account.

To perform a self-deploying mode deployment using Windows Autopilot:

- Create an Autopilot profile for self-deploying mode with the desired settings. In Microsoft Intune, this mode is explicitly chosen when creating the profile. Note that this mode isn't available using the Microsoft Store for Business.
- Ensure that the profile has been assigned to the device before attempting to deploy that device.
- Self-deploying mode requires devices with TPM 2.0 and Windows 10 version 1903 or later.

Some interaction might be required under certain circumstances. If only wireless connectivity is available, the wireless network must be selected. If multiple languages are pre-installed, a language must be selected.



As discussed previously, the Autopilot process requires that the device has Windows 10 or Windows 11 installed. This feature allows you to re-image and provision a 8.1 device for Windows Autopilot user-driven mode using a single, native Configuration Manager task sequence. This process allows a device that was traditionally managed with images to transition to device using modern methods.

In order to facilitate this, a special task sequence must be used to deploy the image to the Windows 8.1 device, which includes delivering a configuration file associated with an Intune profile. The profile(s) must be created in Microsoft Intune before the configuration files are created. Once the profiles are set up, use PowerShell (Administrator) to create the configuration file.




### Windows Autopilot for pre-provisioned deployment

Starting with Windows 10 version 1903, Windows Autopilot can also provide a capability that enables partners or IT staff to pre-provision a Windows PC so that it's fully configured and business-ready. From the end user's perspective, the Windows Autopilot user-driven experience is unchanged, but getting their device to a fully provisioned state is faster.


The process for configuring a pre-provisioned deployment is as follows:

1. Enable the **Windows Autopilot for pre-provisioned deployment** option in the desired Autopilot Profile.
2. Connect (ethernet required for pre-provision) and boot the device. At the first OOBE screen press, the Windows key five times.
3. In the additional dialog options, select **Windows Autopilot provisioning**.
4. Verify the device information. If changes are needed, complete them in Intune, and select refresh to re-download the updated information.
5. Select Provision to provision the device.
6. When the process is complete, select Reseal.


### Windows Autopilot Reset

In many environments, you regularly need to reset devices to their initial states after they've been in use for some time. For example, an organization might provide temporary employees with Windows devices, which the organization must reset for every new user. Organizations must also reset the computers in training rooms after each class. With traditional deployment, you would need to redeploy the Windows image each time you reset a device to its initial state. Windows Autopilot Reset enables you to achieve this goal without redeploying a Windows image. It removes all personal files, apps, and settings, and it resets a Windows device to its initial state from the lock screen. It can also deploy organizational apps and settings by using Intune or another MDM solution so that a device is ready to use after the Windows Autopilot Reset.

Windows Autopilot Reset supports two scenarios:

- Local reset
- Remote reset

#### Local Windows Autopilot Reset

Local Windows Autopilot Reset uses Windows reset functionality. You can use local Windows Autopilot Reset regardless of how you're currently managing a device. It preserves device name, Azure AD membership, and MDM enrollment.

By default, local Windows Autopilot Reset is disabled in Windows, which helps ensure that it doesn't start by accident. To enable local Windows Autopilot Reset, you must set the **DisableAutomaticReDeploymentCredentials** policy to **0** (false).

After enabling local Windows Autopilot Reset, you can start it by pressing _Ctrl+Windows logo key+R_ when you're at the Windows lock screen. Only users with administrative permissions can start local Windows Autopilot Reset.

#### Remote Windows Autopilot Reset

To initiate a remote Windows Autopilot Reset, you can leverage an MDM service such as Microsoft Intune. This method eliminates the necessity for IT personnel to physically visit each individual machine in order to commence the reset procedure. By following these steps, you can use Intune to initiate the remote Windows Autopilot Reset process:

1. In Microsoft Intune admin center, navigate to **Devices** > **Windows**.
2. Select the device for which you want to initiate a remote Windows Autopilot Reset.
3. Select **More** (the ellipsis) and then select **Autopilot Reset** to start the reset.


# Troubleshoot Windows Autopilot

Completed100 XP

- 5 minutes

When troubleshooting Windows Autopilot, it's important to verify the following key factors:

- **Configuration:** Has Azure AD and Microsoft Intune (or an equivalent MDM service) been configured as specified in Windows Autopilot configuration requirements?
- **Network connectivity:** Can the device access the services described in Windows Autopilot networking requirements?
- **Autopilot OOBE behavior:** Where only the expected out-of-box experience screens displayed? Was the Azure AD credentials page customized with organization-specific details as expected?
- **Azure AD join issues:** Was the device able to join Azure AD?
- **MDM enrollment issues:** Was the device able to enroll in Microsoft Intune (or an equivalent MDM service)?

### Troubleshoot Autopilot OOBE issues

If the expected Autopilot behavior doesn't occur during the out-of-box experience (OOBE), it's useful to see whether the device received an Autopilot profile and what settings that profile contained. Depending on the Windows release, there are different mechanisms available to do that.

You can use the Event Tracing for Windows (ETW) can be used to capture detailed information from Autopilot and related components. The resulting ETW trace files can then be viewed using the Windows Performance Analyzer or similar tools.

Information about the Autopilot profile settings is stored in the registry on the device after they're received from the Autopilot deployment service. These settings can be found at HKLM\SOFTWARE\Microsoft\Provisioning\Diagnostics\Autopilot.

To see details related to the Autopilot profile settings and OOBE flow, Windows adds event log entries. These logs can be viewed using Event Viewer, navigating to the log at Application and Services Logs –> Microsoft –> Windows –> Provisioning-Diagnostics-Provider –> Autopilot. The following events might be recorded, depending on the scenario and profile configuration.

Expand table

|Event ID|Type|Description|
|---|---|---|
|100|Warning|"Autopilot policy [name] not found." This event is typically a temporary problem, while the device is waiting for an Autopilot profile to be downloaded.|
|171|Error|"AutopilotManager failed to set TPM identity confirmed. HRESULT=[error code]." This event indicates an issue performing TPM attestation, needed to complete the self-deploying mode process.|
|172|Error|"AutopilotManager failed to set Autopilot profile as available. HRESULT=[error code]." This event is typically related to event ID 171.|

### Windows Autopilot Diagnostics

Windows Autopilot can now aggregate many of the troubleshooting techniques listed into a more easily readable format to isolate issues that occur. This function can be executed from a PowerShell command directly on the device.

Open PowerShell command and enter the following (Accept download prompts):

PowerShellCopy

```
Set-ExecutionPolicy ByPass
Install-Script Get-AutoPilotDiagnostics -force
Get-AutoPilotDiagnostics -Online
```

Once connected to the tenant with an account that has appropriate credentials, through the GraphAPI extensions for Intune, a list of policies, apps, and status is displayed.

### Troubleshoot Azure AD join issues

The most common issue joining a device to Azure AD is related to Azure AD permissions. Ensure the correct configuration is in place to allow users to join devices to Azure AD. Errors can also happen if the user has exceeded the number of devices that they're allowed to join, as configured in Azure AD.

Typically displayed on a "Something went wrong" error page, the error code 801C0003 signifies that the attempt to join Azure AD was unsuccessful.

### Troubleshoot Intune enrollment issues

[See this article](https://learn.microsoft.com/en-us/troubleshoot/mem/intune/device-enrollment/troubleshoot-device-enrollment-in-intune) for assistance with Intune enrollment issues. Common issues include incorrect or missing licenses assigned to the user or too many devices enrolled for the user.

When encountering the error code 80180018, it's accompanied by an error page titled "Something went wrong." This specific error indicates a failed MDM enrollment process.

### Troubleshoot Device Import

If you experience a scenario where importing a device CSV file results in no action and a _'400' error appears in network trace with error body "Cannot convert the literal '[DEVICEHASH]' to the expected type 'Edm.Binary'_ error appears, the device hash within the file is either corrupted or the hash might not be properly padded in the file. To resolve this issue, a minor edit to the file might be necessary to ensure the device hash is in the correct format.

For more information, see [Troubleshooting Windows Autopilot (level100/200)](https://aka.ms/AA6d57a) and [Troubleshooting Windows Autopilot](https://aka.ms/AA80h34).



2. 

You're preparing for an Autopilot deployment in your organization and need to gather device hardware IDs. Which method can you use to obtain these IDs?

Use the windows autopiliot hardware id script


