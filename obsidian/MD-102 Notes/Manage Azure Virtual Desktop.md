
This module will teach you to manage Azure Virtual Desktop, Microsoft's cloud-based virtual desktop infrastructure (VDI) solution. Azure Virtual Desktop lets you provide your users with a personalized, secure Windows 10 experience from anywhere, on any device. In this module, you'll learn about the key features of Azure Virtual Desktop, how to set up and manage the service, and how to configure and secure Azure Virtual Desktop PCs for your users. Whether you're new to Azure Virtual Desktop or already have experience with the service, this module will provide the knowledge and skills to effectively manage and optimize your Azure Virtual Desktop environment. So let's get started!

## Learning Objectives

- Describe the key features of Azure Virtual Desktop
- Describe the Azure Virtual Desktop management experience
- Describe the Azure Virtual Desktop security model
- Describe the Azure Virtual Desktop deployment options


Azure Virtual Desktop, a cloud-based desktop and app virtualization service on Microsoft Azure, offers access to remote desktops and apps across various devices, including Windows, Mac, iOS, Android, and Linux. It also supports most modern browsers for accessing experiences hosted on Azure Virtual Desktop.



This Aloows you to connect to a Virtual Desktop Environment over a web browser similar to Microsoft 365. Azure Virtual Desktop is available for eligible Microsoft 365 license holders at no extra cost, with only Azure resource usage fees applicable. Existing Windows or Microsoft 365 licenses can be used for Windows 10 Enterprise and Windows 7 Enterprise desktops and apps, and eligible Microsoft Remote Desktop Services (RDS) Client Access License (CAL) customers have access to Windows Server Remote Desktop Services desktops and apps at no extra cost.




Azure Virtual Desktop is a cloud-based service for desktop and application virtualization. It operates within the cloud infrastructure, offering users secure and remote access to their desktop environments and applications from various devices and locations.

With Azure Virtual Desktop running on Azure, you can:

1. Establish a multi-session Windows 11 or Windows 10 environment that offers a comprehensive Windows experience with scalability.
2. Deploy Microsoft 365 Apps for enterprise and optimize them for multi-user virtual scenarios.
3. Migrate your existing Remote Desktop Services (RDS) and Windows Server desktops and applications to any device.
4. Virtualize both desktop environments and individual applications.
5. Administer desktops and applications across various Windows and Windows Server operating systems through a unified management platform.

### Key Capabilities

With Azure Virtual Desktop, establish a scalable and flexible environment:

- Create a comprehensive desktop virtualization environment within your Azure subscription, eliminating the need for gateway servers.
- Publish host pools as needed to support diverse workloads.
- Use your own image for production workloads or test from the Azure Gallery.
- Save on costs with pooled, multi-session resources. The Windows - and Windows - Enterprise multi-session capabilities, exclusive to Azure Virtual Desktop and the Remote Desktop Session Host (RDSH) role on Windows Server, allow for a significant reduction in virtual machines and operating system overhead while maintaining resource availability for users.
- Offer individual ownership with personal (persistent) desktops.
- Implement autoscale to automatically adjust capacity based on time of day, specific weekdays, or fluctuating demand, aiding in cost management.

## To deploy and manage virtual desktops:

- Use the Azure portal, Azure CLI, PowerShell, and REST API to configure host pools, create app groups, assign users, and publish resources.
- Publish full desktops or individual remote apps from a single host pool, establish separate app groups for distinct user sets, or assign users to multiple app groups to minimize the number of images.
- Utilize built-in delegated access for role assignment and diagnostic collection to better understand configuration or user errors as you manage your environment.
- Employ the new Diagnostics service for error troubleshooting.
- Manage only the image and virtual machines, not the infrastructure. There's no need for personal management of Remote Desktop roles, as with Remote Desktop Services, just the virtual machines in your Azure subscription.

## Assign and connect users to virtual desktops:

- Once assigned, users can use any Azure Virtual Desktop client to access their published Windows desktops and applications. Connect from any device via a native application on your device or the Azure Virtual Desktop HTML5 web client.
- Securely connect users through reverse connections to the service, eliminating the need to open inbound ports.




| **Aspect**        | **Azure Virtual Desktop (AVD)**        | **Microsoft 365**                        |     |
| ----------------- | -------------------------------------- | ---------------------------------------- | --- |
|                   |                                        |                                          |     |
|                   |                                        |                                          |     |
| **Purpose**       | Virtualized desktops and apps.         | Productivity and collaboration tools.    |     |
| **Primary Focus** | Desktop and app virtualization.        | Cloud-based productivity suite.          |     |
| **Usage Model**   | Cloud-hosted VDI for any device.       | SaaS model for apps and services.        |     |
| **Scalability**   | On-demand scaling of virtual desktops. | User-based licenses with cloud storage.  |     |
| **Access**        | Secure access to virtual desktops.     | Anytime access to Office apps and files. |     |
| **Dependency**    | Requires Azure infrastructure.         | Independent of Azure (but integrates).   |     |


## Use Azure CLI and Azure PowerShell with Azure Virtual Desktop

There's an Azure CLI extension and an Azure PowerShell module for Azure Virtual Desktop that you can use to create, update, delete, and interact with Azure Virtual Desktop service objects as alternatives to using the Azure portal. They're part of [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/what-is-azure-cli) and [Azure PowerShell](https://learn.microsoft.com/en-us/powershell/azure/what-is-azure-powershell), which cover a wide range of Azure services.

This article explains how you can use the Azure CLI extension and an Azure PowerShell module, and provides some useful example commands.

### Azure CLI extension and Azure PowerShell module

Here are the names of the Azure CLI extension and Azure PowerShell module, and links to our reference documentation:

- Azure CLI: [`az desktopvirtualization`](https://learn.microsoft.com/en-us/cli/azure/desktopvirtualization)
    
- Azure PowerShell: [`Az.DesktopVirtualization`](https://learn.microsoft.com/en-us/powershell/module/az.desktopvirtualization)
    

Both Azure CLI and Azure PowerShell are available to use in the [Azure Cloud Shell](https://learn.microsoft.com/en-us/azure/cloud-shell/overview) natively in the Azure portal with no installation, or you can install them locally on your device for Windows, macOS, and Linux.

To learn how to install Azure CLI and Azure PowerShell across all supported platforms, see the following links:

- Azure CLI: [How to install the Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
    
- Azure PowerShell: [Install the Azure Az PowerShell module](https://learn.microsoft.com/en-us/powershell/azure/install-az-ps)


Correct. Depth mode fully allocates users on one VM before moving to the next, ensuring optimal performance.



