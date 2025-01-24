


The Configuration Manager client installation on a Windows computer allows not only the site to manage the device, but ultimately allows both the IT administrator and the end user to benefit from what it can provide.

#### Benefits of the Configuration Manager client

On the admin side, the client installation enables you to track software present on the device, provide inventory information in relation to hardware, and manage and deploy the OS and LoB applications. With innovations in cloud management, many of these features are no longer restricted to use within the network perimeter.

For an end user, some of the potential benefits include a feature rich self-service catalog of software that empowers the user to choose software to install and the ability to configure his/her working hours to ensure interruptions are minimized.

#### Client Deployment Options

To successfully manage a Windows computer using Configuration Manager, you can deploy the client several ways. Below are some of the most used methods:

- **Client push. This** method enables you to deploy the client directly from the Configuration Manager console. Devices can be discovered through various methods, however the most common is by using Active Directory LDAP integration to locate devices in a particular OU. Once discovered, these objects can have client push initialized, which copies the files to the source computer and initiates the install automatically. One consideration with using client push for larger scale deployments is an increase in network traffic from the initial copy process.
    
- **Manual deployment**: This method usually involves the manual deployment of client installation source files accompanied by a script file containing the install parameters. The installation of the agent is typically executed from the ccmsetup.exe file, however it's also possible to install the client from the MSI that is part of the client files. When installed using either option, there are various client installation parameters that dictate how the client will be installed. These parameters make up part of the scripted install. While the manual scripted install achieves the desired results, when not used through an automation tool, this process can be somewhat time consuming as a delivery mechanism. Below shows an example of a CCM Setup command line.
    
    Windows Command PromptCopy
    
    ```
    Ccmsetup.exe  SMSSITECODE=AUTO CCMLOGMAXSIZE=10000 CCMLOGMAXHISTORY=2
    ```
    
- **OS deployment**. This method is one of the most common ways to deliver the client. When installing and setting up Windows using a task sequence, you can slip-stream the Configuration Manager client into the Windows setup and provide it with the necessary installation parameters. To use this method, the client must be installed when a device is built for the first time (or rebuilt), therefore it isn't appropriate for existing devices.
    
- **Microsoft Intune**. One of the more modern methods to facilitate co-management, Intune drives Configuration Manager client installation and registers the device with the Cloud Management Gateway. After it's installed, you can manage each respective workload from either Intune or Configuration Manager.




After you install the Configuration Manager client on the Windows devices and are connected to your site, you can monitor and manage the device directly inside the Configuration Manager console.

From within the Configuration Manager console, there are a number in-built features (status) that can alert you if a client is experiencing issues or could require further attention:

- **Client online status**: The site considers a device **online** if it's connected to its assigned management point. To indicate that the client is online, it sends ping-like messages to the management point. If the management point does not receive a message in five minutes, the site considers the client **offline**.
    
- **Client activity**: The site considers the client **active** if it has communicated with Configuration Manager in the past seven days. The site considers the client **inactive** if it hasn't done the following actions in seven days:
    
    - Requested policy update.
    - Sent a heartbeat message.
    - Sent hardware inventory.
- **Primary User**: From the ECM console, you can see at a high-level what Configuration Manager believes to be the primary user of this device. This metric is calculated over a 60-day period of the most frequent logins.
    
- **Operating System Build**: Data exposed from the inventory performed on the machine enables you to see the OS version of a device without having to connect to or perform any remote management.
    
- **Client check**: The state of the periodic evaluation that the Configuration Manager client runs on the device. The evaluation checks the device and can remediate some of the problems it finds. You can configure remediation not to run on specific devices, for example, a business-critical server. If there are additional items that you want to evaluate, use Configuration Manager compliance settings to monitor additional configurations. Device remediation is an example of a workload that can be utilized through co-management to enable the client to be evaluated, regardless of how the device was brought into the hierarchy. Windows Intune also offers device compliance on the path to modern management, but the subset of noncompliance actions is still evolving. For this reason, co-management using Configuration Manager for remediation is often the most appropriate choice in most advanced scenarios, such as making file or configuration changes to allow remediation for compliance.


When the Configuration Manager client installs on a device and successfully assigns it to a site, you see the device in the **Assets and Compliance** workspace in the **Devices** node. Once in here, the device is likely to join one or more collections from which to be actively managed from.

#### What is a Collection?

Collections are a way for Configuration Manager to represent devices or users that have some degree of commonality. This can be derived from a query, such as OS Type, exclusively placed together, or the same application present. Once in a collection, you can perform several tasks, such as target a deployment or run a report.

When a device is either in a collection or selected directly from the devices pane, there are many management actions that you can access from the right click context menu. Some options can be selected on a per collection basis or the individual object. Below outlines some of the more common options you can review.

Expand table

|Client Action|Description|
|---|---|
|Start Resource Explorer|Review inventory information about a device, such as OS information, memory, and applications installed.|
|Start Policy Retrieval|Execute some of the previous client actions locally, direct from the site server.|
|Add to a collection|Add the client directly to a collection, such as an installation collection from the object itself.|
|Client Settings RSOP|Review current client setting for a given endpoint.|