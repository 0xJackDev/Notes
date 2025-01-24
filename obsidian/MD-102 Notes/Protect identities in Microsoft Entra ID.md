As the number of different sets of credentials that one should manage increases, password security becomes weaker and weaker. Users often use the same or similar passwords for their private email accounts, social networks, and business accounts. This results in a scenario, where a security breach of any user’s digital identity can jeopardize all other identities. Because of this, it’s recommended that you use more authentication methods when authenticating against business resources and alternative methods for authentication. In addition, you should use technologies that can monitor user identities and user account behavior and proactively work to protect and prevent attacks.

#### Objectives

After this module, you should be able to:

- Describe Windows Hello for Business
- Describe Windows Hello deployment and management
- Describe Microsoft Entra ID Protection
- Describe and manage self-service password reset in Microsoft Entra ID
- Describe and manage multi-factor authentication

Windows Hello for Buisness replaces password with strong two-factor authentication on PCs and mobile devices. This authentication consists of a new type of user crential that is tied to a device used 



Windows Hello addresses the following problems with passwords:

- Strong passwords can be difficult to remember, and users often reuse passwords on multiple sites.
- Server breaches can expose symmetric network credentials (passwords).
- Passwords are subject to replay attacks.
- Users can inadvertently expose their passwords due to phishing attacks.

With Windows Hello, users can authenticate to:

- A Microsoft account
- An Active Directory account
- A Microsoft Entra account
- Identity Provider Services or Relying Party Services that support Fast ID Online (FIDO) v2.0 authentication (in progress)



After initial two step verifcation of the user during enrollment, Windows hello is setup on the users device and The User can set a Gesture which can be biometric such as a fingerprint. Or it can be a PIN th euser provides the gesture to verify their identity. Windows hello Authenticates users that way

As an admin you can create policies to manage Windows hello for Buisness use on Windows based devices that connect to your organization




### Biometric sign-in

Windows Hello provides reliable, fully integrated biometric authentication based on facial recognition or fingerprint matching. Windows Hello uses a combination of special infrared (IR) cameras and software to increase accuracy and guard against spoofing. Major hardware vendors are shipping devices that have integrated Windows Hello-compatible cameras. Fingerprint reader hardware can be used or added to devices that don’t currently have it. On devices that support Windows Hello, an easy biometric gesture unlocks users’ credentials.

- **Facial recognition**. This type of biometric recognition uses special cameras that see in IR light, which allows them to reliably tell the difference between a photograph or scan and a living person. Several vendors are shipping external cameras that incorporate this technology, and major laptop manufacturers are incorporating it into their devices, as well.
- **Fingerprint recognition**. This type of biometric recognition uses a capacitive fingerprint sensor to scan your fingerprint. Fingerprint readers have been available for Windows computers for years, but the current generation of sensors is more reliable and less error prone. Most existing fingerprint readers (whether external or integrated into laptops or USB keyboards) work with Windows.

Windows stores biometric data that is used to implement Windows Hello securely on the local device only. The biometric data doesn’t roam and is never sent to external devices or servers. Because Windows Hello only stores biometric identification data on the device, there’s no single collection point an attacker can compromise to steal biometric data.



Deploying Windows Hello There is three models


- Cloud Only. This is for organizations who have cloud identies I.E ENTRA ID and dont access on-premises resources. 
- On-Premises: you should use Group Policy to deploy and configure Windows Hello for Business.
- Hybrid:  In the hybrid model, you should choose which mechanisms (Group Policy or Intune) you'll use.





### Manage Windows Hello for Business with Intune

In Microsoft Intune, Windows Hello for Business can be deployed as a part of a device configuration profile. These profiles are used to configure various settings on Windows 10 and later devices. With device configuration profiles in Intune, you can enable or disable usage of Windows Hello for Business, and also configure the following settings:

- Minimum PIN length
- Maximum PIN length
- Lowercase letters in PIN
- Uppercase letters in PIN
- Special characters in PIN
- PIN expiration (days)
- Remember PIN history
- Enable PIN recovery
- Use a Trusted Platform Module (TPM)
- Allow biometric authentication
- Use enhanced anti-spoofing, when available
- Certificate for on-premises resources

You can also configure Windows Hello for Business settings in device enrollment policies on Intune. This enforces similar configuration settings as listed above, during device enrollment to Intune.



To manage Windows Hello With group policy you need a Windows 10 or later workstation to run the Group Policy Managment Console.


### Windows Hello for Business certificate

A Windows Hello for Business certificate is an authentication credential used in certificate-based Windows Hello for Business deployments. The certificate is a digital identity for a user or device issued by a trusted certificate authority (CA) within an organization's public key infrastructure (PKI). When a user attempts to authenticate, the Windows Hello for Business certificate is presented to verify their identity, and the system checks the certificate's validity against the issuing CA. Using a Windows Hello for Business certificate provides several benefits, such as enhanced security through strong cryptographic mechanisms, easier management of user credentials, and seamless integration with existing PKI infrastructure. It enables organizations to take advantage of passwordless authentication while maintaining high levels of security and compliance.

This certificate has an expiration date, which depends on how long you've set it up in the Windows Hello for Business authentication certificate template. To avoid any authentication issues caused by expired certificates, the Windows certificate auto-enrollment was improved to renew them before they expire. So, you won't have to worry about failing to authenticate due to expired certificates anymore!

Besides protecting resources such as devices, documents, and other critical types of data, it’s necessary to protect user identities, as well. Most of today’s successful cyber attacks are based on identity theft. This makes identity protection, especially of user accounts that have privileges, important for organizations of all sizes.

Each computer user today has at least five, and often more than five, identities (or accounts) for accessing different local or internet-based resources. For example, a typical user has personal accounts with Microsoft, Google, or Apple for emails; social accounts on Facebook and X; and a business account on LinkedIn. Added to this, a typical information worker usually has one or more business accounts that they use on information systems in the organization where they work. Because of all this, a typical user must remember several sets of credentials to be able to access the personal and business resources that they use. This usually leads to a situation where most of the passwords for these accounts are similar or, in the worst case, even the same. This fact greatly increases the risk of identity theft. If one set of credentials is stolen or discovered in any way, it’s highly likely that the other identities of the same user will be at a severe risk.

Because of this, it’s necessary to have an identity protection strategy in each organization. Identity protection is a set of technologies that you implement in your organization that helps you to proactively monitor user behavior, especially during authentication, and to take actions if risk or vulnerability is detected.

 ### Microsoft Entra ID Protection 
 is a Microsoft implementation of identity protection technology targeted at users of Microsoft 365 and other Microsoft cloud services. It’s a feature of the Microsoft Entra ID P2 license.

Microsoft Entra ID Protection provides you with the ability to:

- Proactively recognize potential security risks and identify vulnerabilities in your organization.
- Automatically apply responses and actions when suspicious activity on one or more identities is detected.
- Properly investigate incidents and take actions to resolve them.

You shouldn't consider Microsoft Entra ID Protection as one more reporting and monitoring utility. With this technology, you can also define risk policies with clearly defined actions that can be taken manually or automatically.

Microsoft Entra ID Protection monitors each user session that authenticates on any of your cloud resources and calculates the potential risk. The risk is based on the user location, the application used to authenticate, the device the user uses, and other factors. For example, Microsoft Entra ID Protection can detect if the same user tries to authenticate from two distant geographic locations in a short period of time. Also, it can detect if a user tries to authenticate from a location where he or she's never authenticated before.


![Screenshot of Microsoft Entra ID Protection remediation.](https://learn.microsoft.com/en-us/training/wwl/protect-identities-azure-acative-directory/media/azure-identity-protection-71fb80d4.png)

Based on a calculated risk, Microsoft Entra ID Protection can notify administrators, try to remediate the risk, increase the authentication security requirements, or take another action defined by the risk policy. The sign-in risk level can be Low and above, Medium and above, and High. For each risk level, you can define actions, such as require multi-factor authentication for signing-in, requiring password change, or blocking access.

Microsoft Entra ID Protection provides you with a dashboard where you can monitor, in real time, which users are flagged for risk, how many risk events have happened, and the potential vulnerabilities in your organization.



# Manage self-service password reset in Microsoft Entra ID


When you use only on-premises AD DS, your users can't reset their forgotten passwords by themselves. AD DS in Windows Server doesn't natively support self-service password reset.


Microsoft Entra ID optionally provides this self password reset functionality If you use Microsoft Entra ID P1 or P2 You can extend this to you local AD DS when you use the self service password reset together with the password writeback functionality When you do this password that users reset in Microsoft entra ID are written back to AD DS on premises This means that a user can change his or her password in bouth a cloud or on premesis event.


Before your users start to use self-service password reset, you must enable this functionality in the Azure portal

The self-service password reset functionality requires that you define alternative methods of authentication for users that have forgotten their passwords. Alternative authentication methods that are supported on Microsoft Entra ID can be:

- Office phone
- Mobile phone
- Alternative email address
- Security questions


 If you choose to use security questions, you must define the number of questions required for each user, and you must also predefine the question pool.

We recommend that you offer at least 10 to 15 available questions and that you require that each user register at least four questions for password-reset functionality. If you don't like the pool of predefined questions, you also can define your own questions in your local language.


- If you have Microsoft Entra ID P1 or P2 or Enterprise Mobility + Security licenses, you already have Microsoft Entra multifactor authentication. Your organization doesn't need anything extra to extend the two-step verification capability to all users. You only need to assign a license to a user, and then you can turn on MFA.
    
- When setting up MFA, consider the following tips:
    
    - Don't create a per-authentication multifactor authentication Provider. If you do, you could end up paying for verification requests from users that already have licenses.
    - If you don't have enough licenses for all your users, you can create a per-user multifactor authentication Provider to cover the rest of your organization.
    - Microsoft Entra Connect is only required if you're synchronizing your on-premises Active Directory environment with a Microsoft Entra directory. If you use a Microsoft Entra directory that isn't synchronized with an on-premises instance of Active Directory, you don't need Microsoft Entra Connect.


### Enable MFA for a single Microsoft Entra user

1. Sign in to the Azure portal as an administrator.
2. Go to **Microsoft Entra ID** > **Users and groups** > **All users**.
3. Select **multifactor authentication**.
4. A new page that displays the user states appears.
5. Find the user you want to enable for Microsoft Entra multifactor authentication. You might need to change the view at the top.
6. Select the checkbox for each user’s name.
7. On the right, under Quick Steps, select **Enable** or **Disable**.
8. Confirm your selection in the pop-up window that appears.

After you enable users, notify them via email. Tell them that they'll be asked to register the next time they sign in. Also, if your organization uses non-browser apps that don't support modern authentication, they need to create app passwords. You can also include a link to the Microsoft Entra multifactor authentication end-user guide to help them get started.


Office Phone, Mobile Phone, Alternative Email address and security questions allow you to self-reset password for the Buisness departmentWindows Hello enables organizations to implement two-factor authentication, while providing an easier authentication experience for users on devices that support biometric sign-in. Windows Hello can be implemented in cloud, on-premises and hybrid environments. Microsoft Entra ID Protection actively monitors authentications, evaluates the circumstances, and calculates potential risk, such as consecutive logins from different locations. Microsoft Entra ID also provides the ability for users to reset their own password, while giving Administrators the ability to configure the criteria required to complete the task. With Microsoft Entra multifactor authentication, organizations can configure users provide two or more credentials (such as a PIN and a mobile phone) to sign in to devices and access resources.