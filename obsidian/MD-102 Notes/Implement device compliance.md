If your devices are managed by Intune, you can define how devices should be configured by using device compliance policies. Compliance policies define conditions that devices must fulfill in order to be compliant and able to access company resources.

### Objectives

After this module, you should be able to:

- Describe device compliance policy
- Deploy a device compliance policy
- Describe conditional access
- Create conditional access policies


An Important Use of the MDM such as Intune is that you can allow access to email and documents only from devices managed by MDM and comply with the company policy. Local data on devices must be encrypted, the use of MFA is and the latest updates are installed



YOu can define COmpany policies by using the Device Security Policy in Microsoft 365 or Device Compliance in Intune YOu can control access to email documents and other cloud apps using conditional access policies

If a device isn't enrolled to Intune, its compliance can’t be evaluated, but you can prevent access to mailboxes, documents, and cloud apps from such devices. If a user tries to access their mailbox from such a device, depending on how you set the policy, the user might be blocked from accessing Microsoft 365 resources or redirected to enroll the device to MDM. Alternatively, the user could be granted access, but Microsoft 365 would report a policy violation.


If a device isnt compliant you can block them if they are then you can allow them to certain things

Alternatively, the user could be granted access, but Microsoft 365 would report a policy violation.



## What is A Compliant device?
Compliance Policies define the rules and settings that should be configured on a device for it to be considered Compliant 

After you configure and deploy a compliance policy you can monitor device compliance status and individual devices that are configured in a expected way.


Before you add a compliance policy to a device it must be first enrolled in Intune. Upon enrollment the device can be added to the device group. If the Compliance Policy is assigned to that group the policy will be asessed on the device. With the compliance status being reported in the portal..


Device compliance policies establish the necessary settings for:

- Passwords
- Encryption
- Jail-broken or rooted devices
- Minimum operating-system version
- Maximum operating-system version
- Maximum Mobile Threat Defense level

When a device enrolls in Intune its information and compliance status is added to Microsoft Entra ID. Compliance Policies are assigned to users rather than devices. Conditional access policies utilize Microsoft entra Information to either block or grant access to email or other data. It is not mandatory to use Compliance policies with conditional access; but compliance polciies can be also employed solely as well. 

Intune compliance policies are created in the Devices section of the Intune admin center. The device compliance dashboard for monitoring can be found under Reports.


By default, when Intune detects a device that isn't compliant, it immediately marks the device as noncompliant. In each compliance policy you can configure actions for noncompliant devices, which provide you with extra flexibility in deciding what to do. For example, in a typical scenario, organizations will block access to company resources from a non-compliant device. However, you can configure a compliance policy that instead allows a non-compliant device to access company resources as long as the device is made compliant within a specified grace period. If compliance isn't achieved by that time, the device will no longer be able to access company resources.


There are two types of noncompliant actions:

- **Notify end users via email**. You can customize an email notification before sending it to the end user. You can customize the recipients, subject, and message body, including company logo, and contact information. Intune includes details about the noncompliant device in the email notification.
- **Mark device noncompliant**. You can specify the number of days after which the device is marked as noncompliant. This can be immediately after the device is flagged as noncompliant, or you can give the user a grace period in which he or she can update the device to make it compliant. If the device is still not compliant after the specified number of days, it will be marked as noncompliant.


Device compliance policies can be used in the following manner:

- **With conditional access**. For devices that comply with policy rules, you can allow those devices to access email and other company resources. If the devices don't comply with policy rules, then they don't get access to company resources.
- **Without conditional access**. You can also use device compliance policies without any conditional access. When you use compliance policies without conditional access, there are no access restrictions to company resources.

### Use Microsoft Entra device groups for policies

It's recommended that you use Microsoft Entra groups for users and devices to apply any type of policies implemented with Intune. You can create a group in Microsoft Entra ID with dynamic membership by specifying a rule to determine membership based on user or device properties. When the attributes of a user or device changes, Microsoft Entra ID evaluates all dynamic groups in a directory to see if the change would trigger any group adds or removes. If a user or device satisfies a rule on a group, they're added as a member of that group. If they no longer satisfy the rule, they're removed from the group.

A group membership rule is used to automatically populate a group with users or devices. This is a binary expression that results in a True or False outcome. The three parts of a simple group membership rule include:

- **Property**. Specifies the object attribute; for example, you can use **user.department** to reference the Department attribute of a user object, or **device.displayName** to reference the **displayName** attribute of a device object.
- **Operator**. Can be one of many supported operators, such as Equals (-eq), Starts With (-startsWith), Contains (-contains), or Match (-match).
- **Value**. The value against which you want to evaluate the property by using the operator.

For example, you would use the following group membership rule to include all devices that were manufactured by Microsoft:

Copy

```
device.deviceManufacturer -eq "Microsoft
```





## Deploy a device compliance policy


Before you can deploy a Device Compliance Policy It must first Have the prerequsits


- Must be licensced for Microsoft Entra ID P1 or P2 and Intune. 
- Must be Andorid, Android Enterprise. IOS, MacOS or Windows 8.1 or later
- - Its devices must be enrolled in Intune to be eligible for compliance management.




Compliance policy settings can be found in the Microsoft Intune admin center, in **Devices** > **Compliance policies**.


# Explore conditional access

Conditional Access is a feature of Enterprise Mobility + Security (EMS). it provides Granular access control to organization data while allowing users to work from essentially any device and location. . Conditional access helps to protect your company’s email and data from the security risks posed by devices that are noncompliant.



Intune and Microsoft Entra ID work together to enable conditional access for mobile devices. Intune provides information about device compliance with Microsoft Entra ID. When Microsoft Entra ID receives a request to access resources, it compares this information to conditional access policies.

- If the conditional access policy says that noncompliant devices can't access a resource, the access request is denied.
- If access is denied, the user is prompted to enroll the device and fix the compliance problems.


You can also set policies in Microsoft Entra ID that allow only domain-joined or Intune-enrolled devices to access resources.

A conditional access policy is a definition of an access scenario using the **When this happens**: **Then do this** pattern.

- **When this happens**. Defines the reason for triggering the conditional access policy. This reason is characterized by a group of conditions that have been satisfied. In conditional access, the two assignment conditions play a special role:
    
    - **Users**. The users performing an access attempt (Who).
    - **Cloud apps**. The targets of an access attempt (What).

These two conditions are mandatory in a conditional access policy. In addition to the two mandatory conditions, you can also include other conditions that describe how the access attempt is performed. Common examples are using mobile devices or locations that are outside your company network.

- **Then do this**. Defines the response of the policy. With a conditional access policy, you control how authorized users (users that have been granted access to a cloud app) can access cloud apps under specific conditions. In your response, you enforce other requirements such as multifactor authentication, a managed device, and others. In the context of conditional access, the requirements the policy enforces are called access controls. In the most restrictive form, your policy can block access.

Conditional access is especially beneficial in certain scenarios.

- **Supporting apps that require multi-factor authentication (MFA)**. Some applications require more protection than others. Conditional access allows you to add a layer of protection for them by requiring MFA when users access them.
- **Requiring MFA for untrusted networks**. In this scenario, it isn't the application itself that requires extra security. Instead, the location from where the access is requested is the concern. In this case, you can require a user accessing data from an untrusted location to provide MFA.
- **Allowing Microsoft 365 access only to trusted devices**. You might decide that you want to allow access to Microsoft 365 services only from devices enrolled in Intune and from PCs joined to the on-premises domain. Conditional access allows you to limit access, by Microsoft 365 app, from devices that don't meet these requirements.


You use conditions and controls to create conditional access policies.

### Conditions

A condition is a rule that Intune checks when performing conditional access. For example, a condition might be “when a device meets the password requirements.” Conditions can be based on the:

- Device platform that is accessing the data.
- Location from where the data is being accessed.
- Client applications that are used to access the data.

### Controls

Controls are the actions that are allowed or disallowed when a condition is met. For example, with the previous condition, a control might be “allow access.” Controls include:

- Blocking access.
- Granting access if one or more requirements are met.

### Configure conditional access

You can configure conditional access from the Intune console in the Microsoft Intune admin center. by opening the **Conditional Access** > **Policies** page. When creating the policy, you assign it to users or groups and can specify any cloud services that are affected by the policy.





Conditional Access is Things like If a Client opens an Open if they are not compliant do this if not do that. 



Compliance Configurations Can be applied to Users to see if theyre device is compliant with the company.



#### Conditional Access and Exchange ActiveSync

Exchange ActiveSync (EAS) is an Exchange synchronization protocol that's optimized to work together with high-latency and low-bandwidth networks. The protocol, based on HTTP and XML, lets mobile phones access an organization's information on a server that's running Microsoft Exchange. Not only does EAS allow mobile phone users to access their email, calendar, contacts, and tasks, it also allows them to continue accessing this information when they're working offline. By default, Exchange ActiveSync is enabled. All users who have an Exchange mailbox can synchronize their mobile device with the Microsoft Exchange server.




