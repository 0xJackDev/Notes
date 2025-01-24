Even with the ability to reset the existing Windows image with Autopilot, sometimes even that isn’t necessary, especially with new devices purchased from an OEM. A new device typically starts with a fresh install of Windows, and what’s typically needed is the correct edition deployed (such as Windows Enterprise or Education), correct configuration and apps. When this is the case, dynamic provisioning can further simplify deployments.

Dynamic provisioning uses a number of transforms to achieve this objective.

Expand table

|Name|Description|
|---|---|
|Windows Subscription Activation|With Windows Subscription Activation, users of Windows Pro can upgrade to Windows Enterprise without needing to enter a product key, nor perform a restart.|
|Provisioning package configuration|By using Windows Configuration Designer, you can create configuration packages that you can deploy to users’ devices that can be used to configure apps and settings on those devices.|
|Microsoft Entra join with automatic MDM enrollment|Using Microsoft Entra join with automatic MDM enrollment, users enter their work or school account details and their device is automatically joined to Microsoft Entra ID and enrolled in MDM. The user’s device is then configured per the organization’s MDM policies.|

### Objectives

After completing this module, you'll be able to:

- Describe how Subscription Activation works.
- Describe the benefits of Provisioning Packages.
- Explain how Windows Configuration Designer creates Provisioning Packages.
- Describe the benefits of using MDM enrollment with Microsoft Entra join.


Activating a Windows subscription is necessary to comply with licensing requirements. Activation links the Windows product key to a particular installation of Windows on a device. It assures software integrity and provides you with access to Microsoft support and a full range of updates. There are three main methods for activation:

- Retail
- OEM
- Microsoft Volume Licensing (volume activation)

Microsoft Volume Licensing customers use Volume Activation Services to assist with activation tasks, which consist of Active Directory–based activation, Key Management Service (KMS), and multiple activation key (MAK) models.

### Current volume activation methods

Enterprise environments use three main types of volume activation models and a service that runs on Windows Server 2016. You can use any or all of the options that are associated with these models, depending on your organization’s needs and network infrastructure, including:

- **Key Management Service (KMS)**. This is a role service that you can use to activate systems within your network from a computer where a KMS host has been installed. By default, volume editions of Windows connect to a system that hosts the KMS service to request activation. No action is required from users.
- **Multiple Activation Key (MAK)**. This method of activation uses product keys that can activate a specific number of computers. You can use MAKs to activate any Windows volume edition.
- **Active Directory-based activation**. This is a role service that allows you to use AD DS to store activation objects, which can help simplify the maintenance of volume activation services for a network. When you use Active Directory-based activation, you don't need a host server, as in KMS, and activation requests process during client computer startup.


### Subscription Activation

Frequently, devices are purchased with Windows Pro already installed with a firmware embedded key. Traditionally, the machine needed to be re-imaged with the correct edition, typically Enterprise edition. Subscription activation removes the need for this, transforming a Windows Pro device into a Windows Enterprise device, without the need to re-image and reboot the device.

You can deploy Windows Enterprise E3/E5/A3/A5 licenses within your organization by using Windows Enterprise Subscription Activation or Windows Enterprise E3 in CSP and Microsoft Entra ID. You can deploy Windows Enterprise licenses in the following ways:

- **Enabling Subscription Activation with an existing Enterprise Agreement (EA)**. If you're an existing EA customer, you can get Windows Enterprise E3 or E5 licenses for free, depending on your EA.
- **Enabling Subscription Activation without an existing EA**. You must purchase the licenses from a cloud solution provider (CSP) before you can assign them.

#### Subscription Activation requirements

To implement Subscription Activation, your organization must meet the following requirements:

- Windows Pro/Pro Education/Enterprise/Education is installed and activated on the devices you want to upgrade.
- An instance of Microsoft Entra ID is available for identity management.
- Devices to upgrade are either Microsoft Entra joined or Microsoft Entra hybrid joined.
- For education, the Education tenant must have an active subscription to Microsoft 365 with a Windows Enterprise license or a Windows Enterprise or Education subscription.

#### How Subscription Activation works

With Subscription Activation users can upgrade their devices from Windows Pro to Windows Enterprise without entering a product key, and without requiring the users to restart their computers. Subscription Activation is possible with Windows Pro or Windows Enterprise. Your organization requires either:

- **An EA or a Microsoft Products and Services Agreement (MPSA)**. When a licensed user signs in using Microsoft Entra credentials that are associated with a Windows 11 Enterprise E3/E5 or A3/A5 license on a device, which meets the above requirements, the operating system switches from Windows Pro to Windows Enterprise. All the appropriate Windows Enterprise features are available. When a user’s Microsoft Entra subscription expires, or you transfer the subscription to another user, the Windows Enterprise device reverts back to Windows Pro edition. This occurs after a grace period of up to 90 days.
- **An Enterprise E3 subscription via a CSP**. Windows Enterprise E3 in CSP delivers, by subscription, exclusive features reserved for Windows Enterprise edition. Windows Enterprise E3 is available through a subscription-based model and delivers Windows Enterprise edition features. In a subscription-based model you pay a monthly fee for using Windows, and you don’t need to buy them before you can start using them. This offering is available through the CSP channel through the Partner Center as an online service. Windows Enterprise E3 in CSP provides a flexible, per-user subscription for small- and medium-sized companies, ranging from one to hundreds of users. As with the previous scenario, when a user signs in with Microsoft Entra credentials that are associated with a Windows Enterprise E3 license, the operating system switches from Windows Pro to Windows Enterprise.

### VDA Subscription Activation

You can also take advantage of subscriptions to Windows Enterprise for virtualized clients. Windows Enterprise E3 and E5 are available for Virtual Desktop Access (VDA) in Microsoft Azure or in another appropriate hosting platform. To support this, you must configure your VMs to enable Windows Enterprise subscriptions for VDA. Both AD DS-joined and Microsoft Entra joined clients are supported.

VDA Subscription Activation also supports Inherited Activation starting with Windows 10, version 1803. It enables a Windows VM to inherit its activation state from the Windows host. When a user with Windows E3 or E5 license creates a Windows VM on their Windows host, the VM inherits the activation state from a host machine.

#### VDA Subscription Activation requirements

To enable Windows Subscription Activation, your VMs must:

- Run Windows 11 Pro
- Be a member of an AD DS domain or Microsoft Entra joined
- Be generation 1
- Be hosted by a Qualified Multitenant Hoster (QMTH), such as Microsoft Azure

#### Inherited activation

Windows virtual machines to inherit activation state from their Windows host. When a Windows user with an E3/E5/A3/A5 license creates a new Windows VM on the Windows host, the VM inherits the activation state.

For further details, visit [Windows Subscription Activation](https://learn.microsoft.com/en-us/windows/deployment/windows-10-enterprise-subscription-activation).



A provisioning package is a method of applying configuration settings to a Windows 10 or later device using either removable media or downloaded directly to the device. They're created using a graphical tool called Windows Configuration Designer (WCD). Similar to the concept of group policies, Administrators use WCD to select options for a specific configuration. WCD then exports a package file containing the settings that can be applied to a Windows 10 or Windows 11 device.

You can use a provisioning package to modify a Windows installation and configure many runtime settings without having to reinstall the Windows operating system. For example, you can use a provisioning package to:

- Configure the Windows user interface.
- Add additional files or apps.
- Adjust connectivity settings.
- Meet mobile network requirements.
- Manage Certificates.
- Comply with security policies.
- Remove installed software.
- Reset the Windows installation to its initial state.

Although you can achieve the same result by deploying a new customized Windows 10 or Windows 11 image, using a provisioning package is faster because the file sizes are small.

In a provisioning package, you can configure many settings such as:

- ComputerAccount
- Certificates
- EditionUpgrade
- Folders
- Policies

For example, by using the ComputerAccount setting, you can specify:

- The name for a Windows computer.
- Which domain the computer is a member of.
- Which organizational unit (OU) you want to create the computer account in.
- Which user account you'll use to add the computer to the domain.

You can use the EditionUpgrade setting to:

- Upgrade Windows Pro to Windows Enterprise edition or Windows Education edition.
- Upgrade Windows Home to Windows Education edition without reinstallation.
- Change a product key.
- Perform activation by using the EditionUpgrade setting.
- Apply runtime settings to a running Windows computer, to an offline Windows image, or during the OS installation.

After you configure the settings in the provisioning package, you export the package to a .ppkg file. During the export, you can choose to encrypt the package and sign it. If the provisioning package is signed, you can allow only packages that are trusted to be applied on a client computer.

You apply the provisioning package by running the .ppkg file, by adding the provisioning package in the Settings app, or by running the **Add-ProvisioningPackage** Windows PowerShell cmdlet.

Provisioning Packages can be beneficial for organizations who don't have a more centralized management tool. However, as Provisioning Packages can be applied offline, they can be beneficial for enterprise organizations in scenarios where internet connectivity is limited or unreliable.

# Use Windows Configuration Designer

Completed100 XP

- 3 minutes

The Windows Assessment and Deployment Kit (Windows ADK) includes a tool called Windows Configuration Designer, which you can use to create provisioning packages.

![Screenshot of the Windows Configuration Designer. Shows Project1 open with the Computer Account option in the left view.](https://learn.microsoft.com/en-us/training/wwl/implement-dynamic-deployment/media/windows-configuration-designer-interface-f5f579a4.png)

You can use the Windows Configuration Designer wizards to configure the following settings:

Expand table

|Step|Description|Desktop wizard|Mobile wizard|Kiosk wizard|
|---|---|---|---|---|
|Set up device|Assign a device name, enter the product key to upgrade Windows, configure shared use, and remove preinstalled software|Yes|Only device name and upgrade key|Yes|
|Set up network|Connect to a wireless network|Yes|Yes|Yes|
|Account management|Enroll the device in Active Directory Domain Services (AD DS), enroll the device in Microsoft Entra ID, or create a local administrator account|Yes|-|Yes|
|Bulk enrollment in Microsoft Entra ID|Enroll the device in Microsoft Entra ID before you use a Windows Configuration Designer wizard|-|Yes|-|
|Add applications|Install applications by using the provisioning package|Yes|-|Yes|
|Add certificates|Include a certificate file in the provisioning package|Yes|-|Yes|
|Configure kiosk account and app|Create a local account to run the kiosk mode app, and specify the app to run in kiosk mode|-|-|Yes|
|Configure kiosk common settings|Set tablet mode, configure welcome and shutdown screens, and turn off timeout settings|-|-|Yes|

You can apply a provisioning package during Windows 11 deployment or after the OS installation.

### Microsoft Entra join with automatic MDM enrollment

The Azure AD/MDM dynamic provisioning method is also cloud-driven and is also based on Microsoft Entra ID P1 or P2 and Microsoft Intune. After you enroll a device in Intune MDM, the MDM enforces compliance with your corporate policies, adds or removes apps, and much more. In addition, the MDM can report a device’s compliance with Microsoft Entra ID; this enables Microsoft Entra ID to allow access to corporate resources or applications secured by Microsoft Entra-only to devices that comply with policies.

Using Azure AD/MDM, you can:

- Join devices to Microsoft Entra ID automatically
- Auto-enroll your users’ devices into MDM services
- Configure the joined devices by using MDM policies

The requirements for implementing the Azure AD/MDM deployment model are:

- Windows 10/11 Pro or Enterprise edition
- An instance of Microsoft Entra ID for identity management
- An appropriate MDM, such as Microsoft Intune

---

## Next unit: Use Microsoft Entra join with automatic MDM enrollment




# Use Microsoft Entra join with automatic MDM enrollment

Completed100 XP

- 2 minutes

Joining a device to Microsoft Entra ID is also considered a method of dynamic deployment. This process can be used for either organization-owned devices (sometimes referred to as CYOD) or user-owned devices (BYOD).

### Organizational-owned devices

Instead of joining a domain using a domain controller, the device is enrolling using Microsoft Entra join. This helps streamline deployment and offer new deployment options. Organizations can support scenarios such as a store-bought PC, which the user self-enrolls with their credentials. During the enrollment process, organizational policies and configurations can be applied to ensure the device meets compliance, and deny enrollment if conditions aren't met. This process is faster and easier than requiring a user to reimage the device, and can be a standard process for IT device provisioning, not just exception use cases.

### User-owned scenarios

MDM enrollment also provides an easy way for users and vendors to use their personal devices to access organizational apps and resources. Users can add their Microsoft work account to Windows and enjoy simpler and safer access to the apps and resources of the organization. IT can enforce certain policies – and users have the option to accept or reject them, but must accept them to get access to resources.

Like organizational-owned devices, the MDM enforces compliance with your corporate policies, adds or removes apps, and much more. In addition, the MDM can report a device’s compliance with Microsoft Entra ID. This check enables Microsoft Entra ID to allow access to corporate resources or applications secured by Microsoft Entra-only to devices that comply with policies.


Correct. After you configure the settings in the provisioning package, you export the package to a .ppkg file. During the export, you can choose to encrypt the package and sign it. If the provisioning package is signed, you can allow only packages that are trusted to be applied on a client computer.