


As modern organizations expand, managing various devices, applications, and data becomes more complex. IT professionals face the challenge of securing corporate assets across remote and hybrid workforces, ensuring that users can safely access the resources they need without compromising security. The **Microsoft Intune Suite** addresses these challenges head-on by offering a comprehensive platform that unifies device management, application security, and user support.

By leveraging the Intune Suite, organizations can streamline their endpoint management processes, enhance security, and implement advanced protection measures such as **Zero Trust Security** and **Endpoint Privilege Management**. In this module, we will explore the key features of the Microsoft Intune Suite and how they can be applied to secure, manage, and monitor devices and applications within your organization.

### Learning objectives

After this module, you should be able to:

- Discover the core features of the Microsoft Intune Suite.
- Apply Zero Trust Security using Microsoft Intune.
- Implement Endpoint Privilege Management.
- Understand enterprise app management.
- Explore advanced analytics for device and app insights.
- Provide remote help to users.
- Deploy Microsoft Tunnel for mobile applications.




## Available add-ons

Some capabilities are available to buy as a standalone add-on. Other capabilities are only available with Intune Plan 2 or the Intune Suite.

The following table provides a list of add-on capabilities and associated Intune Plans. For information about Microsoft Intune Plans and pricing, see [Intune Plans and pricing](https://aka.ms/IntuneSuitePricing).

Expand table

|Capability|Standalone add-on|Intune Plan 2|Intune Suite|
|---|---|---|---|
|Endpoint Privilege Management|✅||✅|
|Enterprise App Management|✅||✅|
|Advanced Analytics|✅||✅|
|Remote Help|✅||✅|
|Microsoft Tunnel for Mobile Application Management||✅|✅|
|Microsoft Cloud PKI|✅||✅|
|Firmware-over-the-air update||✅|✅|
|Specialized devices management||✅|✅|

## Key features

- **Endpoint Privilege Management**: This feature allows you to manage and control administrative privileges on Windows 10 devices. It helps you reduce the risk of malware and other security threats by limiting the number of users with administrative access.
- **Enterprise App Management**: This feature enables you to manage and secure applications on Windows 11 devices. It helps you control access to applications and data, ensuring that only authorized users can access sensitive information.
- **Advanced Analytics**: This feature provides insights into device and application usage, helping you identify potential security risks and compliance issues. It helps you make informed decisions about your organization’s security posture.
- **Remote Help**: This feature allows you to provide remote assistance to users who are experiencing technical issues. It helps you troubleshoot problems quickly and efficiently, reducing downtime and improving user satisfaction.
- **Microsoft Tunnel for Mobile Application Management**: This feature enables you to secure and manage mobile applications on iOS and Android devices. It helps you protect sensitive data and ensure compliance with your organization’s security policies.
- **Microsoft Cloud PKI**: This feature provides a cloud-based public key infrastructure (PKI) service that helps you secure your organization’s digital assets. It helps you protect sensitive information and ensure the integrity of your data.
- **Firmware-over-the-air update**: This feature allows you to update the firmware on Windows 10 devices remotely. It helps you keep your devices up to date and secure, reducing the risk of security vulnerabilities.
- **Specialized devices management**: This feature enables you to manage and secure specialized devices, such as point-of-sale terminals and kiosks. It helps you protect sensitive data and ensure compliance with industry regulations.

By using the Microsoft Intune Suite and its add-ons, you can enhance your organization’s device management, security, and compliance capabilities, ensuring that your digital infrastructure remains secure and resilient in the face of evolving threats and challenges.




### Applying Zero Trust security using the Microsoft Intune Suite

**Zero Trust** is a security framework that assumes threats can come from anywhere, both inside and outside the network. It requires continuous verification of users, devices, and applications before granting access to corporate resources. The **Microsoft Intune Suite** plays a key role in implementing a Zero Trust security model by integrating with other Microsoft security solutions to enforce strict access control, device compliance, and identity verification.

### How Zero Trust works in Modern IT

With the increasing adoption of remote and hybrid work environments, corporate networks are more dispersed than ever. This makes traditional perimeter-based security models insufficient. **Zero Trust** assumes that any device or user could be compromised, so access must be continuously evaluated. The Intune Suite helps organizations secure devices, users, and applications with a comprehensive approach to ensure that only trusted entities can access critical resources.

### Key features for implementing Zero Trust with Microsoft Intune

- **Conditional Access Policies**:  
    **Conditional Access** integrates with **Microsoft Entra ID** (formerly Azure Active Directory) to continuously evaluate risks associated with users, devices, locations, and apps. Access is only granted when specific conditions are met, such as the device being compliant with company policies, the user being authenticated via multifactor authentication (MFA), or access requests coming from secure locations.
    
- **Device Compliance Policies**:  
    Intune enables IT administrators to enforce device compliance rules, ensuring that only secure and managed devices can access corporate data. These policies can enforce encryption, require passcodes, and check for the latest security updates. Devices that don’t meet the compliance criteria are automatically restricted from accessing corporate resources.
    
- **App Protection Policies**:  
    App protection policies allow IT to enforce security settings at the application level, even on unmanaged devices (BYOD). These policies ensure that corporate data within apps is encrypted, isolated from personal data, and shared only within approved channels. This helps prevent data leakage, particularly in environments where personal devices are used for work.
    
- **Endpoint Privilege Management**:  
    A key feature of the Intune Suite, **Endpoint Privilege Management** enforces least-privilege access by granting temporary administrative privileges for specific tasks. This minimizes the risk of privilege escalation attacks and reduces the attack surface by ensuring that users only have the access they need for specific tasks.
    
- **Integration with Microsoft Defender for Endpoint**:  
    Microsoft Defender for Endpoint works in tandem with Intune to provide threat detection and response capabilities. Devices are continuously monitored for threats, and actions can be taken automatically to block compromised devices from accessing corporate resources.

### How Intune enables Zero Trust

- Automatically does


With **Conditional Access** policies in place, only compliant devices are allowed to access financial systems, and all devices are monitored in real-time for potential threats through **Microsoft Defender for Endpoint**. Any suspicious activity or non-compliance results in immediate restrictions, ensuring that sensitive financial data remains secure, regardless of where or how employees access it.





Endpoint Privilege Management (EPM) Improves IT support for companies and end users by streamlining how privileges are managed. It can reduce the burden on the IT team for handling repeated privledge requests and increases efficency by automating temporary admin access based on predefined policies. 
Every time a privilege is elevated, the system automatically logs when and why the privilege was granted, for how long, and by whom. This audit trail allows IT teams to monitor privileged access in real-time, detect unusual activity, and ensure that all elevated tasks align with corporate security policies. In case of an audit or security review, these detailed records serve as proof of compliance, showing that privilege management is tightly controlled.


## Role-based access controls for Endpoint Privilege Management

To manage Endpoint Privilege Management, your account must be assigned an Intune role-based access control (RBAC) role that includes the following permission with sufficient rights to complete the desired task:

- **Endpoint Privilege Management Policy Authoring** – This permission is required to work with policy or data and reports for Endpoint Privilege Management, and supports the following rights:
    
    - View Reports
    - Read
    - Create
    - Update
    - Delete
    - Assign
- **Endpoint Privilege Management Elevation Requests** - This permission is required to work with elevation requests that are submitted by users for approval, and supports the following rights:
    
    - View elevation requests
    - Modify elevation requests

You can add this permission with one or more rights to your own custom RBAC roles, or use a built-in RBAC role dedicated to managing Endpoint Privilege Management:

- **Endpoint Privilege Manager** – This built-in role is dedicated to managing Endpoint Privilege Management in the Intune console. This role includes all rights for _Endpoint Privilege Management Policy Authoring_ and _Endpoint Privilege Management Elevation Requests_.
    
- **Endpoint Privilege Reader** - Use this built-in role to view Endpoint Privilege Management policies in the Intune console, including reports. This role includes the following rights:
    
    - View Reports
    - Read
    - View elevation requests

In addition to the dedicated roles, the following built-in roles for Intune also include rights for _Endpoint Privilege Management Policy Authoring_:

- **Endpoint Security Manager** - This role includes all rights for _Endpoint Privilege Management Policy Authoring_ and _Endpoint Privilege Management Elevation Requests_.
    
- **Read Only Operator** - This role includes the following rights:
    
    - View Reports
    - Read
    - View elevation requests




## Remote help 

The **Remote Help** feature in the **Microsoft Intune Suite** enables IT professionals to provide real-time support to users, no matter where they're located. As organizations increasingly adopt hybrid and remote work models, this feature allows IT teams to offer efficient, secure assistance to end users without needing physical access to their devices.


- **Enable Remote Help for your tenant**: By default, Intune tenants aren't enabled for Remote Help. If you choose to turn on Remote Help, its use is enabled tenant-wide. Remote Help must be enabled before users can be authenticated through your tenant when using Remote Help.
    
- **Use Remote Help with unenrolled devices**: Remote Help is supported on enrolled devices that also need to be Microsoft Entra registered devices. This setting is disabled by default. To allow Remote Help on devices that aren't enrolled in Intune, you must turn on this setting.
    
- **Requires Organization login**: To use Remote Help, both the helper and the sharer must sign in with a Microsoft Entra account from your organization. You can't use Remote Help to assist users who aren't members of your organization.
    
- **Compliance Warnings**: Before a helper connects to a user's device, the helper will see a non-compliance warning about that device if it's not compliant with its assigned policies.
    
- **Role-based access control**: Admins can set RBAC rules that determine the scope of a helper's access, such as:
    
    - The users who can help others and the range of actions they can do while providing help. For example, who can run elevated privileges while helping.
    - The users who can only view a device, and who can request full control of the session while assisting others.
- **Monitor active Remote Help sessions, and view details about past sessions**: In the Microsoft Intune admin center, you can view reports that include details about who helped who, on what device, and for how long. You can also find details about active sessions. An administrator can also reference audit log sessions created for Remote Help in Intune under **Tenant Administration** > **Audit Logs**.
    
    For unenrolled devices, auditing the Remote Help sessions is limited.


# Deploy Microsoft Tunnel for mobile applications

Completed100 XP

- 4 minutes

### Microsoft Tunnel for Mobile Application Management (MAM) in the Microsoft Intune Suite

The **Microsoft Tunnel** is a powerful VPN gateway solution integrated within the **Microsoft Intune Suite**, designed to provide secure access to on-premises resources from mobile devices. By using **Microsoft Tunnel**, IT administrators can create a secure connection for mobile users, enabling them to access corporate apps and resources without requiring full device enrollment, making it useful for **BYOD** (Bring Your Own Device) scenarios.

As organizations shift towards remote and hybrid work, employees increasingly access corporate resources from various locations and devices. **Microsoft Tunnel** enables IT administrators to provide secure remote access to internal company resources while maintaining a high level of security and management control. This is especially beneficial in environments where employees are using personal devices, as it allows them to securely connect to internal applications without requiring full device control.


