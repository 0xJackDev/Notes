
Mobile Application Management (MAM) is a crucial aspect of mobile device management, and this module will give you an introduction. The module will cover several key considerations for implementing MAM, including its benefits, challenges, and use cases.

Intune Mobile Application Management (MAM) refers to the suite of Intune management features you can use to publish, push, configure, secure, monitor, and update mobile apps for your users. MAM protects an organization's data within an application by using Microsoft Intune app protection policies that help protect your company data and prevent data loss. Your employees use mobile devices for both personal and work tasks. While making sure your employees can be productive, you want to prevent data loss, intentional and unintentional. You'll also want to protect company data that is accessed from devices that aren't managed by you. You can use Intune app protection policies independent of any mobile-device management (MDM) solution. This independence helps you protect your company's data with or without enrolling devices in a device management solution. By implementing app-level policies, you can restrict access to company resources and keep data within the purview of your IT department.

By the end of this module, you'll have a comprehensive understanding of Mobile Application Management, including its benefits, challenges, and best practices. You'll be equipped with the knowledge and skills to effectively implement and manage MAM policies in Configuration Manager and Intune and secure your organization's mobile apps and data.

### Objectives

After this module, you should be able to:

- Explain Mobile Application Management
- Understand application considerations in MAM
- Explain how to use Configuration Manager for MAM
- Use Intune for MAM
- Implement and manage MAM policies

Intune Mobile Application Management (MAM) refers to the suite of Intune management features you can use to publish, push, configure, secure, monitor, and update mobile apps for your users. MAM protects an organization's data within an application by using Microsoft Intune app protection policies that help protect your company data and prevent data loss.

If you use MAM without enrollment (MAM-WE), a work or school-related app that contains sensitive data can be managed on almost any device, including personal devices in bring-your-own-device (BYOD) scenarios. Many productivity apps, such as the Microsoft Office apps, can be managed by Intune MAM.

Your employees use mobile devices for both personal and work tasks. While making sure your employees can be productive, you want to prevent data loss, intentional and unintentional. You'll also want to protect company data that is accessed from devices that aren't managed by you. You can use Intune app protection policies independent of any mobile-device management (MDM) solution. This independence helps you protect your company's data with or without enrolling devices in a device management solution. By implementing app-level policies, you can restrict access to company resources and keep data within the purview of your IT department.

Intune MAM supports two configurations:

- **Intune MDM + MAM:** IT administrators can only manage apps using MAM and app protection policies on devices that are enrolled with Intune MDM.
- **MAM without device enrollment:** MAM without device enrollment (MAM-WE) allows IT administrators to manage apps using MAM and app protection policies on devices not enrolled with Intune MDM. This means apps can be managed by Intune on devices enrolled with third-party Enterprise Mobility Management (EMM) providers. Also, apps can be managed by Intune on devices enrolled with third-party EMM providers or not enrolled with an MDM at all.

You can create mobile app management policies for Office mobile apps that connect to Microsoft 365 services. You can also protect access to Exchange on-premises mailboxes by creating Intune app protection policies for devices with Outlook for iOS and Android-enabled devices with hybrid Modern Authentication. Before using this feature, make sure you meet the Outlook for iOS and Android requirements. App protection policies aren't supported for other apps that connect to on-premises Exchange or SharePoint services.

The important benefits of using app protection policies are:

- **Protecting your company data at the app level**. Because mobile app management doesn't require device management, you can protect company data on both managed and unmanaged devices. The management is centered on the user identity, which removes the requirement for device management.
- **End-user productivity isn't affected, and policies don't apply when using the app in a personal context**. The policies are applied only in a work context, which gives you the ability to protect company data without touching personal data.

There are additional benefits to using MDM with app protection policies, and companies can use app protection policies with and without MDM at the same time. For example, consider an employee that uses both a phone issued by the company, and their own personal tablet. The company phone is enrolled in MDM and protected by app protection policies while the personal device is protected by app protection policies only. MDM makes sure that the device is protected. Some examples:

- You can require a PIN to access the device, or you can deploy managed apps to the device. You can also deploy apps to devices through your MDM solution, to give you more control over app management.
    
- App protection policies make sure that the app-layer protections are in place. For example, you can:
    
    - Require a PIN to open an app in a work context
    - Control the sharing of data between apps
    - Prevent the saving of company app data to a personal storage location

#### Supported platforms for app protection policies

App protection policies are only supported by Android and iOS. When you enroll Windows devices with Intune, you can use Windows Information Protection, which offers similar functionality.




# Examine considerations for mobile application management

Completed100 XP

- 3 minutes

Intune provides a robust set of mobile application protection policies enabled for Intune-managed apps. These policies provide comprehensive protection to mobile apps and data without requiring complete device management. The following are some of the key benefits of using Intune-managed apps:

- **Restrict copy-and-paste and save-as functions:** Intune-managed apps can be configured to restrict copy-and-paste and save-as functions, which help prevent accidental data leakage or unauthorized data sharing.
- **Configure web links to open inside the Intune Managed Browser app:** IT administrators can configure web links to open inside the Intune Managed Browser app, ensuring that sensitive corporate data isn't accessed through a less secure web browser.
- **Enable multi-identity use and app-level conditional access:** Intune-managed apps enable multi-identity use, meaning users can have multiple identities within a single app. Additionally, app-level conditional access ensures that access to sensitive data is granted only to authorized users and devices.
- **Apply data loss prevention policies without managing the user's device:** With Intune-managed apps, data loss prevention policies can be applied without managing the user's entire device. This approach provides an extra layer of security without compromising on user experience.
- **Enable app protection on devices managed with 3rd party EMM tools:** Intune-managed apps can be enabled with app protection, even on devices managed with 3rd party EMM tools. This functionality ensures that apps and data are always secure, regardless of the device management strategy being used.

One challenge many Intune administrators face is tracking which apps do or don’t support MAM policies. To overcome this challenge, Intune provides an app protection policy report enabling administrators to view a comprehensive list of all apps with MAM policies enabled. This report makes it easy to stay on top of app protection policies and ensure that all corporate data is fully secured.

You can enable your apps to use app protection policies by using either the Intune App Wrapping Tool or the Intune App SDK.

#### Intune App Wrapping Tool

The App Wrapping Tool is used primarily for internal line-of-business (LOB) apps. The tool is a command-line application that creates a wrapper around the app, which then allows the app to be managed by an Intune app protection policy. When protecting an app provided by an independent software vendor (ISV), it's important to clarify if the ISV will still support the wrapped app. You don't need the source code to use the tool, but you do need signing credentials.

 Note

The App Wrapping Tool does not support apps in the Apple App Store or Google Play Store. It also doesn't support certain features that require developer integration.

Reasons to use the App Wrapping Tool:

- Your app doesn't have built-in data protection features
- Your app is simple
- Your app is deployed internally
- You don't have access to the app's source code
- You didn't develop the app
- Your app has minimal user authentication experiences

#### Intune App SDK

The Intune App SDK is designed mainly for customers who have apps in the Apple App Store or Google Play Store, and want to be able to manage the apps with Intune. However, any app can take advantage of integrating the SDK, even line-of-business apps.

Reasons to use the SDK:

- Your app doesn't have built-in data protection features
- Your app is complex and contains many experiences
- Your app is deployed on a public app store such as Google Play or Apple's App Store
- You're an app developer and have the technical background to use the SDK
- Your app has other SDK integrations
- Your app is frequently updated

#### Apps without app protection policies

When apps are used without restrictions, company and personal data can get intermingled. Company data can end up in locations like personal storage or transferred to apps beyond your purview and result in data loss. The arrows in the preceding diagram show unrestricted data movement between both corporate and personal apps, and to storage locations.

![Diagram shows unrestricted data movement between both corporate and personal apps, and to storage locations.](https://learn.microsoft.com/en-us/training/wwl-azure/execute-mobile-application-management/media/mobile-device-corporate-personal-data-9ff783fc.png)

You can use app protection policies to prevent company data from saving to the local storage of the device. You can also restrict data movement to other apps that aren't protected by app protection policies. App protection policy settings include:

- Data relocation policies like Prevent Save As, and Restrict cut, copy, and paste.
- Access policy settings like Require simple PIN for access, and Block managed apps from running on jailbroken or rooted devices.

#### Data protection with app protection policies

![Illustration shows the layers of protection that mobile device management and app protection policies offer together.](https://learn.microsoft.com/en-us/training/wwl-azure/execute-mobile-application-management/media/mobile-device-isolated-corporate-data-8386c158.png)

The preceding illustration shows the layers of protection that MDM and app protection policies offer together.

The MDM solution:

- Enrolls the device
- Deploys the apps to the device
- Provides ongoing device compliance and management

App protection policies add value by:

- Helping protect company data from leaking to consumer apps and services
- Applying restrictions like save-as, clipboard, or PIN, to client apps
- Wiping company data from apps without removing those apps from the device

#### Data protection with app protection policies on devices managed by a Mobile Device Management solution

![Diagram illustrates how the data protection policies work at the app level without mobile device management.](https://learn.microsoft.com/en-us/training/wwl-azure/execute-mobile-application-management/media/mobile-device-isolated-corporate-data-policy-d6816879.png)

The preceding diagram illustrates how the data protection policies work at the app level without MDM.

For BYOD devices not enrolled in any MDM solution, App protection policies can help protect company data at the app level. However, there are some limitations to be aware of:

- You can't deploy apps to the device. The end user has to get the apps from the store.
- You can't provision certificate profiles on these devices.
- You can't provision company Wi-Fi and VPN settings on these devices.


App protection policies can be applied to apps running on devices that may or may not be managed by Intune. In many organizations, it’s common to allow end users to use both Intune MDM managed devices, such as corporate owned devices, and un-managed devices protected with only Intune app protection policies, such as bring your own devices (BYOD).

Because Intune app protection policies are targeted to a user’s identity, the protection settings for a user typically apply to both enrolled (MDM managed) and non-enrolled devices (no MDM). Therefore, you can target an Intune app protection policy to either Intune enrolled or un-enrolled iOS and Android devices. You can create one protection policy for un-managed devices in which strict data loss prevention (DLP) controls are in place, and a separate protection policy for MDM managed devices, where the DLP controls may be a little more relaxed.