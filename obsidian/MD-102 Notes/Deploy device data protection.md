
Windows Information Protection or WIP is a set of tech that protects organizations from accidental or malicious data leaks. its a type of DLP tool.

After this module, you should be able to:

- Describe Windows Information Protection
- Plan for Windows Information Protection usage
- Implement and use Windows Information Protection
- Describe the Encrypting File System (EFS)
- Describe BitLocker

---

## Next unit: Explore Windows Information Protection



## Windows information protection

In modern enterprises the increase in collaboration between both internal and external users and proliferation of employee-owned devices known as BYOD has increased the risk of data loss. 

Organizations use DLP systems to overcoome limitation so fa systems that are based on authentication and authorization. A DLP system automatically detects and controls data that should be protected

 A DLP system requires:

- Rules that identify and categorize data that needs protection.
- Software applications such as Microsoft Exchange or Microsoft SharePoint to scan data to see if it matches rules.
- A way to define what actions applications must carry out when they find data that matches a rule.

The challenge of a DLP system is that the more rules you create, the more likely workers will feel the system is preventing them from getting work done, and they'll find ways to bypass the system. For example, they might share data by emailing links to an unprotected system instead of attaching files to an email system that contains DLP protection. Despite improvements to DLP in Microsoft SharePoint Online and Microsoft Exchange Online, such as allowing users to override the rules, the experience can be jarring to users and interrupt their natural workflow.


#### Information Rights Management

As we said before, enterprises need to protect data after it leaves the company. To meet this need, systems based on Information Rights Management (IRM) are used to make protection an inherent part of documents. An employee can create a document and then determine the level of protection that should apply to the document, such as preventing unauthorized users from opening the document. In some scenarios, protection can also be applied automatically, based on conditions that the administrator defines.

IRM systems require setting up both client and server environments. The client app that opens a document is responsible for processing protection rules after checking with the server component of the system to check for authorization updates.

Neither IRM nor DLP is sufficient in the scenario where an employee leaves the organization with a personal device or simply decides that they no longer want to allow the organization to manage the personal device. The best-case option, in this case, is to delete organizational data from the personal device. Protection systems implemented in Microsoft 365 platform, allows you to do this. These systems allow you to create rules based on which apps can access organizational data. It also allows you to decide which data those apps can access.

Azure Rights Management (Azure RMS) extends protection for data beyond a user’s device through an IRM system that integrates with WIP, a key part of Azure Information Protection. Intune allows control over user actions with protected data, even outside the organizational environment.

Additionally, apps that can tell the difference between organizational or personal data, known as enlightened apps, allow you to apply WIP rules on organization-owned data only, while leaving personal data intact. This means, for example, that an employee can safely use Microsoft Word on a personal device for both business and personal documents, without fear of losing their personal data when they leave the organization.




# Plan Windows Information Protection

Completed100 XP

- 7 minutes

Planning for the usage of WIP in your organization is crucial because it not only helps to address the shortcomings of DLP and IRM systems but also enables you to explore innovative approaches to data management.

WIP helps you to overcome several common challenges by providing:

- **Separation between personal and corporate data:** Users don't need to choose which app to use for which data.
- **Additional protection to LOB apps:** You can add protection without modifying the app.
- **Ability to perform a selective wipe:** You can remove corporate data from a device without removing personal data.
- **Audit reporting:**. WIP gives you the ability to track and report on policy issues and the actions performed in response to policy violations.
- **Management system integration:** WIP integrates with Intune, Endpoint Configuration Manager, and other Mobile Device Management (MDM) systems. These benefits help you protect enterprise data in various scenarios:
- **Encrypt data on a device:** When you are copying or downloading organizational data from SharePoint, Microsoft OneDrive, network shares, or other locations using a device that is managed by using WIP policies, WIP encrypts the data on the device, even if the device is personally owned.
- **Control which apps can access corporate data:** Apps that you've included on the Allowed Apps list can access organizational data, while apps that aren't on the list have more limited capabilities. For example, if the policy is set to Override mode, when a user tries to copy data from an allowed app to a personal app, a warning notice will ask for confirmation to perform a potentially unsafe action.
- **Enlightened apps allow users to work with both personal and corporate data:** Some apps, such as Word, automatically detect when a file contains corporate data and should be WIP-protected, and they maintain that protection when saving a file locally or on removable media. This protection is maintained even if the file name changes or if the data is stored with unencrypted personal data.
- **Prevent use of personal apps and services:** You can prevent accidental release of organizational data to public spaces and social media by preventing users from using applications such as personal OneDrive to store files. You can also prevent users from copying data from allowed apps to X or Facebook.
- **Remove corporate data from lost or stolen devices, or devices owned by ex-employees:** You can remove organizational data from, and unenroll, any devices that are enrolled in Intune, including personal devices, even if the device is lost or stolen. This is a necessary protection when employees leave the company and it doesn’t affect personal data.

# Implement and use Windows Information Protection

Completed100 XP

- 15 minutes

When you use Windows Information Protection, organizational data automatically encrypts when data downloads to or opens on a local device. Encryption protects the file data and associates the data with your enterprise identity.

WIP policies then specify which trusted apps can use and manipulate that data. Enlightened apps such as Word or Microsoft Excel can work with organizational and personal data. When creating WIP policies, you can set four WIP-protection modes, which the following table lists, for managing that access.

Expand table

|Mode|Description|
|---|---|
|Block or Hide overrides|Prevents employees from performing data-sharing actions when blocked by the policy. In some Microsoft documentation, this is referred to as Hide overrides mode.|
|Allow overrides|Warns employees when they're performing a potentially risky action, but they can choose to complete the action. The action records to the audit log.|
|Silent|Works like Allow overrides mode, except that it only records any action that an employee can override to the audit log. Any action that would be blocked is still blocked.|
|Off|WIP is turned off and doesn't protect data.|

#### Create a WIP policy in Intune

When you create policies in Intune, you can define which apps are protected, the level of protection provided, and how to find organizational data on your network.

To create a WIP policy in Intune, perform the following steps:

1. **Sign in to the Microsoft Intune admin center**.
2. Navigate to **Apps** > **App protection policies**.
3. In the **App protection policies** pane, select **Add a policy**, and then fill in the following fields:
    - **Name**. Enter a name for the policy.
    - **Description**. Enter a description for the policy.
    - **Platform**. Select the platform for the policy.
    - **Enrollment state**: Choose Without enrollment for MAM or With enrollment for MDM.
4. Select **Protected apps** and then select **Add apps**. You can add these types of apps:
    - **Recommended apps**. These are enlightened apps that work with WIP.
    - **Store apps**. These are apps that are available from Microsoft Store.
    - **Desktop apps**. These are signed Windows desktop apps. Please note that an application might return access denied errors after removing it from the list of protected apps. Rather than remove it from the list, you should uninstall and reinstall the application or exempt it from WIP policy.

#### Allowed and exempt apps

The process for adding an app rule varies slightly depending on the type of rule template that you use. The rule templates are:

- **Recommended App**. Recommended apps are enlightened apps that work with WIP.
- **Store App**. This is for apps that are available from Microsoft Store.
- **Desktop App**. This is for signed Windows desktop apps.

For detailed information about how to add each type of app to the Allowed apps list, refer to the “Add apps to your Allowed apps list” topic in “Create a Windows Information Protection (WIP) policy with MDM using the Endpoint Manager admin center.

After you add the apps that you plan to protect, you'll need to decide on the protection mode that you want to use. When creating and verifying your policies with a group of test users, consider the best practice of using the Silent or Allow overrides mode before using the Block mode. In doing so, you can confirm that these are the correct apps to have on your Allowed apps list.

#### Corporate identity

Your corporate identity identifies organizational data from apps that you protect with WIP. For example, emails coming from your organizational domain would be identified as organizational, and WIP policies would be applied. For this reason, you typically want to add all the domains from which you send emails.

You add your corporate identity by typing your domain name or multiple domain names separated by the pipe character (|) in the Corporate identity field.

#### Network perimeter

WIP needs to know where the apps can find and access organizational data on your network, also known as the network boundary. There is no default set of locations or automatic way to define these locations. You must add them to your WIP policies, and you can add as many locations as you require.

When you add a network boundary definition, you choose the type of boundary; based on that choice, you provide the definition in a specific format. You can also configure the policy to tell Windows if some boundary lists, such as the lists of proxy servers or IP addresses, are definitive or if searching for other servers or IP addresses on your network is allowed.

The following table describes the different boundary type options.

Expand table

|Network element|Description|
|---|---|
|Cloud resources|Specifies URLs for cloud-based resources or applications such as SharePoint Online or Microsoft Visual Studio Codespace that should be treated as containing organizational data. You can make multiple entries by using the format **URL1**\|**URL2**.|
|Protected domains|Defines DNS suffixes for domains that should be treated as protected. Multiple entries are allowed by using the format domainname1,domainname2; for example, corp.adatum.com,sales.adatum.com.|
|Network domains|Defines the DNS suffixes that are used within your environment. Multiple entries are allowed by using the format domainname1,domainname2; for example, corp.adatum.com,sales.adatum.com.|
|Proxy servers|Specifies external-facing proxy server addresses and ports where WIP should protect traffic. For example, proxy.adatum.com:80;proxy2.adatum.com:137.|
|Internal proxy servers|Specifies proxy servers that devices use to reach cloud-based resources. Uses the same format as enterprise proxy servers.|
|IPv4 ranges|Specifies the range of Internet Protocol version 4 (IPv4) addresses used in your network. Enter by using the format startingaddress-endingaddress, with multiple ranges separated by commas. This network element is required if you don't specify an enterprise Internet Protocol version 6 (IPv6) range.|
|IPv6 ranges|Specifies the range of IPv6 addresses used in your network. This network element is required if you don't specify enterprise IPv4 ranges, and it uses the same format as IPv4.|
|Neutral resources|Specifies authentication redirection endpoints for your company, such as Active Directory Federation Services endpoints. Enter by using the format **URL1**\|**URL2**.|

#### Data Recovery Agent (DRA) certificate

As described earlier, WIP will encrypt enterprise data when it’s on local drives. If the encryption key is lost or revoked, you can't recover the data. By adding a DRA certificate, you provide a public key that will encrypt the local data, which will allow you to unencrypt that data later if necessary.

If you don’t already have an Encrypting File System (EFS) DRA certificate, you'll need to create one and upload it to your policy before you can deploy it.

For more information, see [Create and verify an Encrypting File System (EFS) Data Recover Agent (DFA) certificate](https://aka.ms/G7280o).

#### Optional WIP-related settings

You can also configure these other WIP policy settings:

- **Revoke encryption keys on unenroll**. Users can't access encrypted organizational data when a device is unenrolled from Intune.
- **Show the Windows Information Protection icon overlay**. Determines if the WIP icon overlays files in File Explorer or in the Save As view.
- **Use Azure RMS for WIP.** Determines whether Azure RMS encryption will be used for WIP. Must have Azure RMS.
- **Use Windows Hello for Business as a method for signing into Windows**. Determines if users can use Windows Hello to sign in to their device and the rules for using Windows Hello.



# Explore Encrypting File System in Windows client

Completed100 XP

- 9 minutes

EFS is a built-in file encryption tool for Windows-based systems. EFS is a component of the NTFS file system, and it uses advanced, standard cryptographic algorithms to allow transparent file encryption and decryption. Through the Windows Information Protection functionality of Windows, EFS functionality is also simulated on volumes that use the FAT32 file system. Any individual or app that doesn't have access to a certificate store that holds an appropriate cryptographic key cannot read encrypted data. You can protect encrypted files even from those who gain physical possession of a computer on which files are stored. Even people who have the authorization to access a computer and its file system cannot view the encrypted data.

Encryption is a powerful addition to any defensive plan. However, you must use additional defensive strategies, because encryption isn’t the correct countermeasure for every threat. Furthermore, every defensive weapon has the potential to harm your data, if you use it incorrectly. When you implement EFS, the most important task is to properly manage EFS certificates for users. Encryption provided by EFS is based on user certificates, and their public and private keys. Without proper certificate management, you can easily get into a situation where encrypted data isn't accessible.

#### Manage EFS certificates

EFS uses public key cryptography to encrypt files. EFS obtains the keys from a user’s EFS certificate, which also might contain private key information. Therefore, you must manage them correctly.

Users need asymmetric key pairs to encrypt data, and they can obtain these keys:

- **From a certification authority (CA)**. An internal or third-party CA can issue EFS certificates. This method provides central management and back up of keys. This is recommended way to issue and manage EFS certificates as it allows you to restore user certificate if it's lost.
- **By generating them**. If a CA is unavailable, Windows will generate a key pair. These keys have a lifespan of 100 years. This method is more difficult than using a CA because there's no centralized management, and users become responsible for managing their own keys. Additionally, recovery is more difficult to manage. However, it’s still a popular method because it requires no setup.

Users can make encrypted files accessible to other users’ EFS certificates. If you grant access to another user’s EFS certificate, that user may make those files available to yet another user’s EFS certificates.

#### Issue a certificate for a DRA

Before starting to use EFS in your organization, it’s very important to issue a certificate for a Data Recovery Agent (DRA). This certificate is used in scenarios where a user who encrypted the file can't or does not want to decrypt it. A user that has a DRA certificate can decrypt any encrypted file in the organization. This applies to all files encrypted after a DRA certificate is issued.

You can issue EFS certificates only to individual users. You cannot issue EFS certificates to groups.

#### CAs can archive and recover CA-issued EFS certificates

If you use CA to issue EFS certificates, you can configure archiving of user’s private key. You should configure this before you start to issue EFS certificates for users. If you don’t use this functionality, users must back up their self-generated EFS certificates and private keys manually. To do this, they can export the certificate and private key to a Personal Exchange File (.pfx), which is password-protected during the export process. This password is required to import the certificate into a user’s certificate store. In Windows, you can also use built-in tool to manage and back up user certificates used for EFS. It is recommended that each user that uses EFS, use this tool to back up his or her certificate, with a private key, to external protected location.

#### Export the client EFS certificate without the private key

If you need to distribute only your public key, you can export the client EFS certificate without the private key to Canonical Encoding Rules (.cer) files. A user’s private key is stored in the user’s profile in the RSA folder, which you can access by expanding **AppData** > **Roaming** > **Microsoft** > **Crypto**. However, please note that because there is only one instance of the key, it is vulnerable to hard-disk failure or data corruption.

#### Export certificates with the MMC Certificates snap-in

The Microsoft Management Console (MMC) Certificates snap-in exports certificates and private keys. The Personal Certificates store contains the EFS certificates. When users encrypt files in remote shared folders, their keys are stored on the file server.

#### How EFS works

The basic EFS encryption functionality works as follows:

- When a user who possesses the necessary key opens a file, the file opens. If a user does not possess the key, the user receives an access-denied message.
- File encryption uses a symmetric key that it encrypts with a user’s public key, which is stored in the file header. Additionally, it stores a certificate with the user’s public and private keys, or asymmetric keys, in the user’s profile. The user’s private key must be available for decryption of the file.
- If a private key incurs damage or is lost, the file cannot be decrypted. If a data recovery agent exists, the file is recoverable. If you implement key archival, you can recover the key and decrypt the file. Otherwise, the file might be lost. The certificate system, which the encryption is based on, is referred to as public key infrastructure (PKI).
- You can archive a user’s certificate that contains his or her public and private keys. For example, you can export it to a USB flash drive, and then keep the USB flash drive in a safe place for recovery if the keys incur damage or are lost.
- A user’s password protects the public and private keys. Any user who can obtain the user ID and password can sign in as that user and decrypt that user’s files. Therefore, an organization’s security practices should include a strong password policy and user education to protect EFS-encrypted files.
- EFS-encrypted files do not remain encrypted when crossing the network, such as when you work with the files on a shared folder. The file is decrypted, and it then traverses the network in an unencrypted state. EFS encrypts it locally if you save it to a folder on the local drive that is configured for encryption. EFS-encrypted files can remain encrypted while traversing a network if you save them to a web folder by using the World Wide Web Distributed Authoring and Versioning (WebDAV) protocol. They can also remain encrypted if you configure the network traffic to be encrypted by using Internet Protocol Security (IPSec).
- EFS supports industry-standard encryption algorithms, including Advanced Encryption Standard (AES). AES uses a 256-bit symmetric encryption key and is the default EFS algorithm.

#### EFS features in Windows 10

Additionally, be aware of the following features when implementing EFS on Windows:

- **Support for storing private keys on smart cards**. Windows includes full support for storing users’ private keys on smart cards. If a user signs in to Windows with a smart card, EFS also can use the smart card for file encryption. Administrators can store their domain’s recovery keys on a smart card. Recovering files is then as simple as signing in to the affected machine, either locally or by using Remote Desktop, and using the recovery smart card to access the files.
- **The Encrypting File System Rekeying Wizard**. The Encrypting File System Rekeying Wizard allows users to choose an EFS certificate, then select and migrate the existing files that will use the newly chosen EFS certificate. Administrators can use the wizard to migrate users in existing installations from software certificates to smart cards. The wizard also is helpful in recovery situations because it’s more efficient than decrypting and re-encrypting files.
- **Group Policy settings for EFS**. You can use Group Policy to control and configure EFS protection policies centrally for an entire enterprise. For example, Windows allows page file encryption through the local security policy or Group Policy.
- **Per-user encryption of Offline Files**. You can use EFS to encrypt offline copies of files from remote servers. When you enable this option, each file in the offline cache is encrypted with a public key from the user who cached the file. Thus, only that user has access to the file, and even local administrators cannot read the file without access to the user's private keys.
- **Selective Wipe**. A feature of Windows in a corporate environment is Selective Wipe. If a device is lost or stolen, an administrator can revoke the EFS key that was used to protect the files on the device. Revoking a key prevents all access to data files that are stored on a user’s device.

EFS allows you to protect and encrypt indivudual Files  Bitlocker encrypts the whole harddrive


#### Compare BitLocker and EFS

As previously noted, both BitLocker and EFS provide encryption functionality. However, these technologies are not the same and don’t have the same purpose. While EFS is focused on providing protection on the file and folder level, BitLocker does that on the volume or disk level. Once you protect the file with EFS, that file stays protected until you (or another person with proper permission) unlock it, and that protection does not depend on file location. On the other hand, files on the drive protected with BitLocker are protected as long as they are on that specific drive. The following table compares BitLocker and EFS-encryption functionality.

Expand table

|BitLocker functionality|EFS functionality|
|---|---|
|Encrypts volumes (the entire operating-system volume, including Windows system files, and the hibernation file).|Encrypts files.|
|Does not require user certificates.|Requires user certificates.|
|Protects the operating system from modification.|Does not protect the operating system from modification.|

#### Device encryption

Device encryption is a built-in Windows feature. By default, device encryption protects the operating system drive and any fixed data drives on the system by using Advanced Encryption Standard (AES) 128-bit encryption, which uses the same technology as BitLocker. You can use device encryption with a Microsoft account or a domain account.

Device encryption is enabled automatically on all Windows 10 and later versions on new devices, so that the device is always protected. Supported devices that you upgrade to Windows 10 or with a clean installation also have device encryption automatically enabled.

#### BitLocker To Go

When a laptop is lost or stolen, the loss of data typically has more impact than the loss of the computer asset. As more people use removable storage devices, they can lose data without losing a computer. BitLocker To Go provides protection against data theft and exposure by extending BitLocker support to removable storage devices, such as USB flash drives. You can manage BitLocker To Go by using Group Policy, from Windows PowerShell, and by using the BitLocker Drive Encryption Control Panel app.

In Windows, users can encrypt their removable media by opening File Explorer, right-clicking the drive, and selecting **Turn On BitLocker**. Users then can choose a method with which to unlock the drive, including using a password or a smart card.

After choosing an unlock method, users must print or save their recovery key. You can configure Windows to store this 48-digit key in Active Directory Domain Services (AD DS) automatically, so that you can use it if other unlocking methods fail, such as when users forget their passwords. Finally, users must confirm their unlocking selections to begin encryption. When you insert a BitLocker-protected drive into your computer, the Windows operating system will detect the encrypted drive and prompt you to unlock it.

#### Microsoft BitLocker Administration and Monitoring (MBAM)

As with any security technology that you implement, centralized management is recommended. You can centrally manage BitLocker by using Group Policy, but with limited functionality. Part of the Microsoft Desktop Optimization Pack, MBAM makes it easier to manage and support BitLocker and BitLocker To Go with full functionality. MBAM 2.5 with Service Pack 1, the latest version, has the following key features:

- Administrators can automate the process of encrypting volumes on client computers across the enterprise.
- Security officers can determine the compliance state of individual computers or even of the enterprise itself.
- Provides centralized reporting and hardware management with Microsoft Endpoint Configuration Manager.
- Reduces help desk workload assisting end users with BitLocker recovery requests.
- End users can recover encrypted devices independently by using the Self-Service Portal.
- Security officers can audit access to recovery key information.
- Windows Enterprise users can continue working anywhere with their corporate data protected.
- Enforces the BitLocker encryption policy options that you set for your enterprise.
- Integrates with existing management tools, such as Endpoint Configuration Manager.
- Offers an IT-customizable recovery user experience.

![Screenshot of Microsoft MBAM prompting for the KeyID and reason for recovering access to an encrypted drive.](https://learn.microsoft.com/en-us/training/wwl/deploy-device-data-protection/media/bitlocker-administration-monitoring-b958cc38.png)





