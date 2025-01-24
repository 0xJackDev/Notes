

# Monitor device profiles in Intune

Completed100 XP

- 3 minutes

Intune includes some features in the Microsoft Intune admin center to help monitor and manage your device configuration profiles. For example, you can check the status of a profile, see which devices are assigned to it, and update the properties of a profile.

### View existing profiles

Complete the following steps to view existing profiles:

1. In the Microsoft Intune admin center, select **Devices**.
2. On the **Devices overview** page, select **Monitor** , then select **Assignment status**.

All your existing profiles are listed, which includes details such as the platform, and shows if the profile is assigned to any devices.

### View details on a profile

After you create your device profile, Intune provides graphical charts. These charts display the status of a profile, such as it being successfully assigned to devices, or if the profile shows a conflict.

1. Select an existing profile and select the **Overview** tab. The top graphical chart shows the number of devices assigned to the specific device profile. For example, if the configuration device profile applies to Windows 10 and later devices, the chart lists the count of the Windows 10 and later devices. It also shows the number of devices for other platforms that are assigned the same device profile. In the example, it shows the count of the non-Windows 10 and later devices.
    
    ![Screenshot of two charts. Top chart titled, Profile assignment status - Windows 10 and later devices.](https://learn.microsoft.com/en-us/training/wwl-azure/oversee-device-profiles/media/intune-profile-assignment-status-2f5eb053.png)
    
    The second graphical chart shows the number of users assigned to the specific device profile. For example, if the configuration device profile applies to Windows 10 and later users, the chart lists the count of the Windows 10 and later users.
    
2. Select the circle in the top graphical chart. The **Device status** opens. The devices assigned to the profile are listed, and it shows if the profile is successfully deployed. Also note that it only lists the devices with the specific platform (for example, Windows 10 and later devices). Close the Device status details.
    
3. Select the circle in the bottom graphical chart. The **User status** opens. The users assigned to the profile are listed, and it shows if the profile is successfully deployed. Also note that it only lists the users with the specific platform (for example, Windows 10 and later devices). Close the User status details.
    
4. Back in the **Profiles** list, select a specific profile. You can also change existing properties:
    
    - **Properties.** Change the name or update any existing settings.
    - **Assignments.** Include or exclude devices that the policy should apply. Choose **Selected Groups** to choose specific groups.
    - **Device status.** The devices assigned to the profile are listed, and it shows if the profile is successfully deployed. You can select a specific device to get even more details, including the installed apps.
    - **User status.** Lists the user names with devices impacted by this profile, and if the profile successfully deployed. You can select a specific user to get even more details.
    - **Per-setting status.** Filters the output by showing the individual settings within the profile and shows if the setting is successfully applied.

### View conflicts

In **Devices** >**All devices**, you can see any policy settings that are causing a conflict. When there's a conflict, you're also shown all the configuration profiles that contain this setting. Administrators can use this feature to help troubleshoot and fix any discrepancies with the profiles.

1. In the Microsoft Intune admin center, select **Devices** >**All Devices**, and then select an existing device in the list. An end user can get the device name from their Company Portal app.
2. Select **Device configuration**. All configuration policies that apply to the device are listed.
3. Select the policy. It shows you all the settings in that policy that apply to the device. If a device has a Conflict state, select that row. In the new window, you see all the profiles, and the profile names that have the setting causing the conflict.

Now that you know the conflicting setting and the policies that include that setting, it should be easier to resolve the conflict.


You must sync your devices with Intune to update them with the latest policies and actions. The **Sync device** action forces the selected device to immediately check in with Intune. When a device checks in, it immediately receives any pending actions or policies that have been assigned to it. This feature can help you immediately validate and troubleshoot policies you’ve assigned, without waiting for the next scheduled check-in.

Complete the following steps to sync a device:

1. In the Microsoft Intune admin center, select **Devices**, then select **All devices**.
2. In the list of devices you manage, select a device, select **More** and then select **Sync**.
3. To confirm, select **Yes**.
4. To see the status of the sync action, choose **Devices** > **Monitor** > **Device actions**.

### Manage settings and features on your devices with Intune policies

Microsoft Intune policies are groups of settings that control features on mobile devices and computers. You create policies by using templates that include recommended or custom settings. Then, you deploy them to device or user groups.

Intune policies fall into the following categories. The category that you use affects how you create and deploy the policy.

- **Configuration policies**. Commonly used to manage security settings and features on your devices, including access to company resources. Get started at Intune device profiles.
- **Device compliance policies**. Define the rules and settings that a device must comply with to be considered compliant by conditional access policies. You can also use compliance policies to monitor and remediate the compliance of devices independent of conditional access.
- **Conditional access policies**. Help secure email and other services, depending on conditions that you enter.
- **Corporate device enrollment policies**. Intune supports the enrollment of corporate-owned iOS devices using the Apple Device Enrollment Program (DEP) or the Apple Configurator tool running on a Mac computer.

When a policy or an app is deployed, Intune immediately begins notifying the device to check in with the Intune service. This step typically takes less than five minutes.

If a device doesn't check in to get the policy after the first notification is sent, Intune makes three more attempts. If the device is offline (such as being turned off, or not connected to a network), it might not receive the notifications. In this case, the device gets the policy on its next scheduled check-in with the Intune service, as follows:

Expand table

|Platform|Check-in frequency|
|---|---|
|iOS|Every 6 hours|
|macOS|Every 6 hours|
|Android|Every 8 hours|
|Windows 11|Every 8 hours|

If the device recently enrolled, the check-in frequency is more frequent, as follows:

Expand table

|Platform|Check-in frequency|
|---|---|
|iOS|Every 15 minutes for 6 hours, and then every 6 hours|
|macOS|Every 15 minutes for 6 hours, and then every 6 hours|
|Android|Every 3 minutes for 15 minutes, then every 15 minutes for 2 hours, and then every 8 hours|
|Windows PCs (enrolled as devices)|Every 3 minutes for 30 minutes, and then every 8 hours|

Users can also open the Company Portal app and sync the device to immediately check for the policy anytime.


# Manage devices in Intune using scripts

Completed100 XP

- 3 minutes

The Intune management extension lets you upload PowerShell scripts in Intune to run on Windows devices, in addition to shell scripts for the macOS. The management extension supplements mobile device management (MDM) capabilities and makes it easier for you to move to modern management.

You can create scripts to run on the devices that provide the capabilities you need. For example, you can create a PowerShell script that installs a legacy Win32 app on your Windows devices, upload the script to Intune, assign the script to a Microsoft Entra group, and run the script on Windows devices. You can then monitor the run status of the script on Windows devices from start to finish.

The Intune management extension has the following prerequisites:

Expand table

|**Windows**|**macOS**|
|---|---|
|Version 1607 or later.|version 10.12 or later|
|Devices must be joined to Microsoft Entra ID, including Hybrid AD joined devices.|Devices are managed by Intune.|
|Automatic MDM enrollment must be enabled in Microsoft Entra ID.|Shell scripts begin with #! and must be in a valid location such as #!/bin/sh or #!/usr/bin/env zsh.|
||Command-line interpreters for the applicable shells are installed.|

### Create a PowerShell script policy for Windows

1. In the Microsoft Intune admin center, select **Devices**.
    
2. In the Policy section, select **Scripts** and select **Add**, then select **Windows 10 and later**.
    
    Adding scripts is similar to the process for creating a profile. After adding a name and description, you'll configure the Script settings.
    
3. In **Script settings**, enter the following properties:
    
    - **Script location**: Browse to the PowerShell script. The script must be less than 200 KB (ASCII).
    - **Run this script using the logged on credentials**: Select Yes to run the script with the user's credentials on the device. Choose No (default) to run the script in the system context. Many administrators choose Yes. If the script is required to run in the system context, choose No.
    - **Enforce script signature check**: Select Yes if the script must be signed by a trusted publisher. Select No (default) if there isn't a requirement for the script to be signed.
    - **Run script in 64-bit PowerShell host**: Select Yes to run the script in a 64-bit PowerShell host on a 64-bit client architecture. Select No (default) runs the script in a 32-bit PowerShell host.
4. Select **Next** and configure scope tags and assignments. Note that PowerShell scripts in Intune can be targeted to Microsoft Entra device security groups or Microsoft Entra user security groups.
    

### Create a shell script policy for macOS

Adding a script for the macOS uses the same steps creating a PowerShell script policy, selecting **macOS** after choosing **Add**. The macOS script settings are slightly different.

1. In **Script settings**, enter the following properties:
    
    - **Upload script**: Browse to the Shell script. The script must be less than 200 KB (ASCII).
    - **Run script as signed-in user**: Select **Yes** to run the script with the user's credentials on the device. Choose **No** (default) to run the script as the root user.
    - **Hide script notifications on devices**: By default, script notifications are shown for each script that is run. End users see an IT is configuring your computer notification from Intune on macOS devices.
    - **Script frequency**: Select how often the script is to be run. Choose **Not configured** (default) to run a script only once.
    - **Max number of times to retry if script fails**: Select how many times the script should be run if it returns a non-zero exit code (zero, meaning success). Choose **Not configured** (default) to not retry when a script fails.
2. Select **Next** and configure scope tags and assignments. Note that shell scripts assigned to user groups apply to any user signing in to the Mac.

