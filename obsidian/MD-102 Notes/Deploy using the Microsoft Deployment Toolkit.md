There are several on-premises methods that have been traditionally used to facilitate OS deployments within organizations. While newer cloud-based solutions have frequently simplified many methods and processes, on-premises tools still have a place in modern management. In this module, we’ll discuss these shifts from traditional to modern management, and where on-premises solutions best fit in today’s enterprise.

### Objectives

After completing this module, you'll be able to:

- Describe the fundamentals of using images in traditional deployment methods.
- Describe the key benefits, limitations, and decisions when planning a deployment of Windows using Microsoft Deployment Toolkit (MDT).
- Describe how Configuration Manager builds upon MDT and how both can work in harmony.
- Explain the different options and considerations when choosing the user interaction experience during deployment, and which methods and tools support these experiences.

Until Windows 11, the method of choice for deploying an OS was typically imaging the device. Imaging is applying a preconfigured OS to a large group of computers. This has historically been the preferred method of large-scale deployments where manual installation methods could be more practical. Traditional methods like imaging are still supported for Windows 11 or later.

### Default and custom images

Administrators must decide whether to use the default Windows image or create a custom image when choosing an image to deploy.

The Windows installation files include the default OS image, install.wim. This image is a basic OS image that contains a standard set of drivers. When you use the default OS image, configuring the OS and installing applications must be done separately after the image is deployed.

Configurations and applications can be included in custom images. Tools such as Deployment Image Servicing and Management (DISM.exe) can be used to service and prepare Windows images. DISM is a command line tool that can capture the image of a reference computer with the desired OS, settings, and applications. DISM can also be used to mount the image and make modifications.

Sysprep is then used to generalize the image prior to deployment. Before deploying a Windows image to new PCs, you must first generalize the image. This process removes computer-specific information such as installed drivers and the computer security identifier (SID). Generalizing the image makes it ready for deployment.

There are advantages and disadvantages to using default and custom images, as outlined in the following chart.

Expand table

|Default Image|Custom Image|
|---|---|
|No need to create an image|Image must be created and maintained|
|Applications and settings must be applied separately|Applications and Settings can be included in custom image|
|One image per architecture (x86/x64) can be used for the organization|The configuration and application requirements (and sometimes hardware) of each group within an organization can typically require several images to be created and maintained|
|Updates to applications don't require the image to be re-built|Updates to applications cause images to become stale, requiring images to be updated or re-created frequently|
|Overall deployment time is typically slower, as configurations must be applied and applications installed after the OS image is deployed|Overall deployment time is typically faster with the configurations and applications included in the image|
|Some applications can be difficult to automate the installation|When applications are installed on the reference machine, they're typically easier to deploy when included with the image|

### Thin versus thick images

When you're choosing how to image, thin and thick images refer to what the image contains beyond the OS. A thin image may be the default image or a custom image with just the OS and a few drivers required to ensure the OS installs correctly. Alternatively, a thick image might be the OS and several applications widely used across the organization.

At first, thick images can appear as a more attractive option. However, thick images become more difficult to manage over time. Eventually, applications require updates, and configuration changes are often needed. With every deployment, these changes and updates must be applied. As the updates accumulate over time, deployment time can significantly increase. With multiple images to support, managing versions of apps and configurations can become difficult. As time passes, the need to rebuild the image increases to the point where it becomes necessary. The effort to rebuild images can negate the time initially saved with thick images.

For these reasons, thin images are recommended, applying configurations and installing applications after deployment. While they take some extra up-front effort, updates become easier to manage, and images don't become "stale" as quickly. Organizations can automate these post-deployment tasks with minimal maintenance to the images themselves using GPOs and device policies to apply configurations using solutions like Endpoint Manager.

### Boot from VHD

Instead of installing the OS directly on the physical drive, Windows 7 and later devices also support boot from VHD. Using tools such as Hyper-V, PowerShell, or the Disk Management console, a `.vhd` or `.vhdx` file can be created. You can apply a Windows image file and boot from it as if it were natively installed on the storage device.



thin OS is just the bare minimum OS and drivers

THICK OS is the OS Plus all needed applications





## Microsoft Deployment Toolkit MDT
The MDT is a unified collection of tools used for automating desktop and server deployments. You can use it to create reference images or as a complete deployment solution.
MDT enables you to manage security and ongoing configuration more easily. MDT builds on top of the core deployment tools in the windows assessment and deployment kit (Windows ADK). MDT provides 

### MDT setup prerequisites

To enable a successful Windows deployment, you must plan and assemble the MDT infrastructure prior to the delivery of the operating system.

Some of the key elements of the architecture of an MDT delivery include:

- **Active Directory Domain Services Environment**. Joins endpoints to Active Directory during the deployment process to a specified OU.
- **Windows 2016 or later server**. Hosts the MDT installation and setup of the deployment share for content that will be used during the capture or deployment process.
- **Windows ADK**. Includes the most recent Windows Assessment and Deployment Kit (ADK) to match the target Windows version of destination clients. This install takes place on the MDT server and supports the creation of boot images to service new client OS installs.
- **Windows Deployment Services (optional)**. Facilitates a network-driven initialization of the OS deployment.
- **Windows Server Update Services (optional)**. Includes a Windows 2016 or 2019 Server to house the Windows Update metadata and connection to Microsoft. The content downloaded can be utilized by MDT to deliver software updates during the OS deployment process.


### Reference images

Creating a reference image is the foundation to standardizing the operating system configuration delivered to your users. You use MDT to create these images with the necessary configuration and build upon some of the prerequisites, such as a deployment share and configuration rules and settings.





### Add an application to the captured image

Before you create an MDT task sequence, you must first add any applications, and scripts you want to install to the MDT build lab share. Select the source files and add the application under the application pane.

If you need to add multiple applications, consider using Windows PowerShell to speed up the process. The following example shows connecting to the deployment share using the MDT PowerShell Support modules and then adding a sample application.



