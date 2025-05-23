

This module will teach you to manage Windows 365, Microsoft's cloud-based PC management solution. Windows 365 lets you provide your users with a personalized, secure Windows 11 experience from anywhere, on any device. In this module, you'll learn about the key features of Windows 365, how to set up and manage the service, and how to configure and secure Windows 365 PCs for your users. Whether you're new to Windows 365 or already have experience with the service, this module will provide the knowledge and skills to effectively manage and optimize your Windows 365 environment. So let's get started!

## Learning Objectives

- Describe the key features of Windows 365
- Describe the Windows 365 management experience
- Describe the Windows 365 security model
- Describe the Windows 365 deployment options
- Describe the Windows 365 licensing model


Windows 365 is a cutting-edge cloud-based service that simplifies how you create and manage virtual machines. It automatically generates a new Windows virtual machine called Cloud PCs for your end users. With Windows 365, each Cloud PC is assigned to an individual user, providing them with a dedicated Windows device. By using Windows 365, you can experience the benefits of Microsoft 365, which include increased productivity, enhanced security, and seamless collaboration. With these features, Windows 365 offers a flexible and scalable solution to support your organization's growth and changing needs.

Windows 365 is available in two editions:

- **Windows 365 Business:** Windows 365 Business is made specifically for use in smaller companies (up to 300 users) who want ready-to-use Cloud PCs with simple management options. There are no licensing prerequisites to set up Windows 365 Business. There are no dependencies on Azure or Active Directory. Purchases are made through the Microsoft 365 admin center or the Windows 365 product site. For more information, see [Getting started with Windows 365 Business and Cloud PCs](https://learn.microsoft.com/en-us/windows-365/business/get-started-windows-365-business).
- **Windows 365 Enterprise:** Windows 365 Enterprise is designed for larger organizations seeking unlimited users to create Cloud PCs. It offers the flexibility to build custom Cloud PCs using your own device images, provides additional management options, and seamlessly integrates with Microsoft Intune. Windows 365 Enterprise utilizes Microsoft Entra ID and AD DS domains to enhance its functionality. For more information, see [What is Windows 365 Enterprise?](https://learn.microsoft.com/en-us/windows-365/enterprise/overview).

## Compare Windows 365 Business and Enterprise

## General comparisons

Expand table

|Capability|Windows 365 Business|Windows 365 Enterprise|
|---|---|---|
|Domain join|Microsoft Entra join without Azure Virtual Network (VNet) Support|Microsoft Entra join without VNet support.  <br>Microsoft Entra join with VNet support.  <br>Hybrid Microsoft Entra ID with VNet support.  <br>For other domain support, see [In development for Windows 365 Enterprise.](https://learn.microsoft.com/en-us/windows-365/enterprise/in-development)|

## Purchasing and licensing comparisons

Expand table

|Capability|Windows 365 Business|Windows 365 Enterprise|
|---|---|---|
|Domain Join|Microsoft Entra join without Azure Virtual Network (VNet) support.|Microsoft Entra join without VNet support.  <br>Microsoft Entra join with VNet support.  <br>Hybrid Microsoft Entra ID with VNet support.  <br>For other domain support, see In development for Windows 365 Enterprise.|
|Purchase channels|Web direct, self-service, Cloud Solution Provider (CSP).|Web direct, Enterprise Agreements (EA), CSP.|
|License assignment|Microsoft 365 Admin Center or the Microsoft Entra admin center.|Microsoft 365 Admin Center or the Microsoft Entra admin center.|
|Licensing requirements|No licensing pre-requirements to buy and deploy Windows 365 Business. Other features (like device management) can be used if users are licensed for Microsoft Endpoint Management.|Each user must be licensed for Windows 10 or 11 Enterprise (when available), Microsoft Endpoint Manager, and Microsoft Entra ID P1.|
|Networking costs|Outbound data/month is based on the RAM of the Cloud PC:  <br>- 2-GB RAM = 12-GB outbound data  <br>- 4-GB or 8-GB RAM = 20-GB outbound data  <br>- 16-GB RAM = 40-GB outbound data  <br>- 32-GB RAM = 70-GB outbound data  <br>Data bandwidth may be restricted when these levels are exceeded.|When providing a network, Networking goes through the customer's Azure VNet and isn't included in the license. [Azure bandwidth pricing](https://azure.microsoft.com/pricing/details/bandwidth/) applies for these network usage costs.  <br>If using a Microsoft-hosted network, the same charges (as described in Windows 365 Business networking charges) apply.|
|User limits|Capped to 300 users per tenant.|No user cap per tenant.|

## Administration comparisons

Expand table

|Capability|Windows 365 Business|Windows 365 Enterprise|
|---|---|---|
|Provisioning|Provisioning is simplified and uses default configurations. Cloud PCs are automatically provisioned with a standard image after a Cloud PC license is assigned.|Provisioning is configurable and customizable to the needs of the organization. Admins select the network, configure user permissions (local admin or not), and assign the policy to a Microsoft Entra group. Cloud PCs are then provisioned by using standard gallery images or custom images (admin choice).|
|Policy management|Not Supported.|Group Policy Objects (GPO) and Intune MDM are supported.|
|Application deployment|Supported only if you have Intune license.|Supported.|
|Windows updates|Default Windows Update for Business settings are configured for users. With an Intune license, these settings can be edited.|Can be managed by using Microsoft Endpoint Manager.|
|Device management|Device management is limited to assigning and unassigning of Cloud PC licenses in the Microsoft Admin Center. Some device management is possible in Microsoft Endpoint Manager if you have an Intune license but Cloud PCs won't be visible in the Windows 365 blade.|Microsoft Intune admin center options, including image management, link and access on-premises resources, granular targeting of policies, resizing Cloud PCs, other user experience settings, and all the policy-based management options available to physical devices.|
|Monitoring|Not supported.|Endpoint Analytics reporting and monitoring, service health, and operational health alerts.|
|Troubleshooting|Not supported|Microsoft Endpoint Manager troubleshooting including the Troubleshooting blade, device management actions, and reprovisioning of Cloud PCs to their initial state.|
|Partner/programmatic access|Not supported|Partners can manage Cloud PCs through Microsoft 365 Lighthouse or restful web APIs (Graph) to support Managed Service Provider tooling for up to 300 users.|
|Universal Print|Not supported.|Supported|

## End-user comparisons

Expand table

|Capability|Windows 365 Business|Windows 365 Enterprise|
|---|---|---|
|Management|Users can restart, reset, rename, and troubleshoot their Cloud PCs on the Windows 365 homepage.|Users can restart, rename, and troubleshoot their Cloud PCs on the Windows 365 homepage.|
|Role|By default, each user is a Standard User on their Cloud PC. To grant Local Administrator permissions to a specific user on a Cloud PC, see [Remote management actions](https://learn.microsoft.com/en-us/windows-365/business/remotely-manage-business-cloud-pcs#remote-management-actions). To grant Local Administrator permissions for Cloud PCs that you create in the future, see [Change organizational default settings](https://learn.microsoft.com/en-us/windows-365/business/change-organization-default-settings).|By default, each user is assigned a standard user role on their Cloud PC. The administrator has the capability to modify this role within the Microsoft Intune admin center.|
|Access|Users can access their Cloud PC at windows365.microsoft.com or by using Microsoft Remote Desktop or the Windows 365 app.|Users can access their Cloud PC at windows365.microsoft.com or by using Microsoft Remote Desktop or the Windows 365 app.|
|Platform|Any platform that supports Microsoft Remote Desktop clients or the Windows 365 app.|Any platform that supports Microsoft Remote Desktop clients or the Windows 365 app.|

## Security comparisons

Expand table

|Capability|Windows 365 Business|Windows 365 Enterprise|
|---|---|---|
|Conditional Access|Conditional Access policies can be deployed only by using Microsoft Entra ID with a Microsoft Entra ID P1 license.|Conditional Access policies can be deployed by using the Microsoft Intune admin center or Microsoft Entra ID.|
|Per-user multifactor authentication (MFA)|Only MFA using Microsoft Entra Conditional Access is supported. Legacy per-user MFA isn't supported.|Legacy per-user MFA is supported for user connections to Microsoft Entra hybrid joined Cloud PCs. It's not supported for user connections to Microsoft Entra joined Cloud PCs.|
|Security baselines|Not supported.|Dedicated Security Baselines can be edited and deployed by using Microsoft Endpoint Manager.|
|Microsoft Defender for Endpoint|Supported if the customer separately has the requisite E5 license.|Integration with Defender for Endpoint. If the customer has an E5 license, all Cloud PCs respond to Defender for Endpoint policies and show up in MDE dashboards.|

### Access cloud PCs

Users can navigate to [https://windows365.microsoft.com](https://windows365.microsoft.com/) to access their Cloud PCs, connecting through Remote Desktop.

![Screenshot of the cloud pc gear, showing; Restart, Reset, Rename, Troubleshoot, and System information.](https://learn.microsoft.com/en-us/training/wwl/manage-windows-365/media/cloud-personal-computer-gear-04bac88c.png)

The Remote Desktop client is available for Windows, macOS, iOS/iPadOS and Android.



The primary setup process for Windows 365 takes place within the Microsoft Intune admin center. Here's a general overview of the fundamental steps required to configure your system for provisioning on-demand Cloud PCs to your users.


1. ## Assign licenses to users Inside of the microsoft entra admin center and add licenses to users or groups 
2. ### Create an Azure network connection. THis is done in the Microsoft Endpoint manager
3. ### Configure a custom device image (optional)
4. ### Create provisioning policies




Managing Cloud PCs is just like managing any other device. You apply configuration profiles and assign apps. You apply quality and feature updates using update rings. You apply security policies in the same manner as physical devices. While you might specify separate policies just for Cloud PCs, the method is no different.

### Remote actions

Most of the same remote actions available on physical devices, are available for Cloud PCs as well. They include:

- Restart
- Sync
- Rename
- Quick Scan
- Full Scan
- Update Windows Defender

There are three remote actions that are unique to Cloud PCs and are available if a Cloud PC is selected.

- Reprovisioning
- Resize
- Collect diagnostics

### Reprovisioning

The Reprovision remote action allows admins to reprovision Cloud PCs. When this action is initiated, the Cloud PC is reset to its initial state. Note, that user data, applications, and customizations aren't automatically deleted - this depends on the specific configuration of the Cloud PC and the policies in place to handle user data during reprovisioning. It's recommended to always ensure data backup before initiating a reprovision.

- You're testing different Cloud PC configurations.
- Your provisioned Cloud PC is misbehaving.
- The user simply wants to start from a fresh Cloud PC.

To reprovision a Cloud PC, perform the following steps:

1. Sign in to the **Microsoft Endpoint Manager admin center**, select **Devices** > **All Devices** > choose a Cloud PC device > **Reprovision**.


Microsoft 365 is Microsofts Cloud platform that allows u to create and use Windows Virtual machines in da cloud. 


Also Custom CLoud PCs are only in windows 365 enterprise.

