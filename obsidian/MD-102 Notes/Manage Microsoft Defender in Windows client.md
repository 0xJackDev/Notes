The Windows Security Center, a component in Windows 11 and later versions, encompasses all facets of security for the operating system, user accounts, and applications on a particular device. The Windows Security Center is an upgraded version of Microsoft Defender anti-malware software. It offers a complete range of security features to keep your Windows device secure for its entire supported lifespan.

Windows Security Center is turned on, by default and it works from the moment you install Windows operating system. It covers the following areas:

- **Virus and threat protection:** help handle all anti-virus and anti-malware tasks.
- **Account protection:** allows you to configure account sign-in options, and Windows Hello sign-in options and Dynamic lock settings.
- **Firewall and network protection:** You can manage Windows Firewall, configure applications that must communicate through firewall and also setup domain profiles for firewall.
- **App and browser control:** In this part of Windows Security Center, you can configure the Microsoft Defender SmartScreen feature that helps you protect a device by proactively checking for unrecognized apps and files from the internet. The SmartScreen feature also works for Microsoft Edge and for Microsoft store apps.
- **Device security:** You can find information about processor core isolation, processor security, TPM and secure boot features.
- **Device performance & health:** You have the ability to verify if Windows is current, and to identify potential issues that could affect the overall health of your device. This includes examining storage capacity concerns, device driver problems, battery life complications, and app or software issues. Additionally, from this point, you can initiate a fresh start for an existing installation of Windows.
- **Family options:** You can review and configure available options for family safety and parental controls.
- **Protection History (Windows 11):** List recent threats and any recommended actions. This option is located under Virus and threat protection in Windows 10.



Windows Defender Credential Guard, was first introduced in Windows 10 Enterprise and Windows Server 2016, employs virtualization-based security to restrict access to sensitive information, allowing only privileged system software to access it. Credential theft attacks, such as Pass-the-Hash or Pass-The-Ticket, can occur due to unauthorized access to these secrets. By safeguarding NTLM password hashes, Kerberos Ticket Granting Tickets, and domain credentials stored by applications, Windows Defender Credential Guard effectively thwarts such attacks.

By enabling Windows Defender Credential Guard, the following features and solutions are provided:

- **Platform security features to protect credentials:** Hardware security NTLM, Kerberos, and Credential Manager take advantage of platform security features, including Secure Boot and virtualization, to protect credentials.
- **Virtualization-based security:** Windows NTLM and Kerberos-derived credentials and other secrets run in a protected environment that's isolated from the running operating system.
- **Better protection against advanced persistent threats:** The credential theft attack techniques and tools used in many targeted attacks are blocked when Credential Manager domain credentials, NTLM, and Kerberos-derived credentials are protected using virtualization-based security. Malware running in the operating system with administrative privileges can't extract secrets that are protected by virtualization-based security. While Windows Defender Credential Guard offers strong protection, advanced persistent threats may still adapt to new attack techniques. For complete security, combining Windows Defender Device Guard with other security strategies and architectures is recommended.

### Enable Windows Defender Credential Guard by using Group Policy

You can use Group Policy to enable Windows Defender Credential Guard. This adds and enables the virtualization-based security features for you if needed. To enable it, follow these steps:

1. From the Group Policy Management Console, go to **Computer Configuration** - **Administrative Templates** - **System** - **Device Guard**.
2. Double-click **Turn On Virtualization Based Security**, and then select **Enabled**.
3. In the Select Platform Security Level box, choose **Secure Boot** or **Secure Boot and DMA Protection**.
4. In the Credential Guard Configuration box, select **Enabled with UEFI lock**, and then select **OK**. If you want to be able to turn off Windows Defender Credential Guard remotely, choose **Enabled without lock**. ![screenshot of Windows Defender Credential Guard Group Policy setting.](https://learn.microsoft.com/en-us/training/wwl/manage-defender-windows-client/media/virtualization-based-security-322010f5.png)

Besides using Group Policy to enable Credential Guard, administrators can also use Microsoft Intune platform to deploy this feature to client computers enrolled to Microsoft Entra ID and Intune. Credential Guard is a part of device configuration profile, when using Endpoint protection profile type. It's available only for Windows 10 and later OS platforms.

![screenshot of Windows Defender Credential Guard.](https://learn.microsoft.com/en-us/training/wwl/manage-defender-windows-client/media/intune-credential-guard-760949ed.png)



USe group policy to deploy Windows Defender crendtial guard

You can configure Microsoft Defender Antivirus with several tools, including:

- Microsoft Intune
- Configuration Manager
- Group Policy
- PowerShell cmdlets
- Windows Management Instrumentation (WMI)

If you use the Microsoft 365 platform, it’s recommended to use Intune to manage Microsoft Defender. To manage Microsoft Defender by using Intune, follow these steps:

1. In the Microsoft Intune admin center, select **Devices**, then select **Windows** platform, then select **Configuration Profiles**.
    
2. Select **Create Profile**.
    
3. Enter the following properties:
    
    - **Platform**: Choose which versions of Windows to include.
    - **Profile type**: Select **Device restrictions**.
4. On the **Configuration settings** tab, expand the **Microsoft Defender Antivirus** item and configure the desired settings.
    

![Screenshot of Windows Defender Antivirus screen.](https://learn.microsoft.com/en-us/training/wwl/manage-defender-windows-client/media/intune-defender-antivirus-1d2f7442.png)

A very important part of Windows Defender is a firewall. You can access firewall settings from Windows Security center or you can find these options in Control Panel, in the Network and Sharing Center and System and Security items. In System and Security, you can configure basic Windows Defender Firewall settings and access the Action Center to view notifications for firewall alerts. In the Network and Sharing Center, you can configure all types of network connections, such as changing the network location profile. You also can configure basic Windows Defender Firewall settings in the Windows Security Center.

You cannot configure all Windows Defender Firewall settings in the Windows Security Center. Some links in the Windows Security Center open the Windows Defender Firewall page in Control Panel.



For Windows computers enrolled in Intune or joined to Microsoft Entra ID, you can use Microsoft Intune to manage settings for Windows Firewall. These settings are part of the Endpoint protection device configuration profile. When you choose to create a new device configuration profile in Intune and select Endpoint protection, you will be presented with settings available for Windows Firewall. You can manage all features discussed later in this unit by using Microsoft Intune. For computers in Microsoft Entra ID, this is the recommended way to manage firewall settings.

### Firewall exceptions

When you add a program to the list of allowed programs, or open a firewall port, you are allowing that program to send information to or from your computer. Allowing a program to communicate through a firewall is like making an opening in the firewall. Each time that you create another opening, the computer becomes less secure.

Generally, it’s safer to add a program to the list of allowed programs than to open a port in the firewall. If you open a port without scoping the port to a specific app, the opening in the firewall stays open until you close the port, regardless of whether a program is using it. If you add a program to the list of allowed programs, you are allowing the app itself to create an opening in the firewall, but only when necessary. The openings are available for communication only when required by an allowed program or computer.

To add, change, or remove allowed programs and ports, you should perform the following steps:

1. In Control Panel, on the Windows Defender Firewall page, in the navigation pane, select **Allow an app or feature through Windows Defender Firewall**.
2. Select **Change settings**.

For example, to view performance counters from a remote computer, you must enable the Performance Logs and Alerts firewall exception on the remote computer.

To help decrease security risks when you open communications:

- Only allow a program or open a port when necessary.
- Remove programs from the list of allowed programs, or close ports when you do not require them.
- Never allow a program that you do not recognize to communicate through the firewall.

#### Multiple active firewall profiles

Windows includes multiple active firewall policies. These firewall policies enable computers to obtain and apply a domain firewall profile, regardless of the networks that are active on the computers. Information technology (IT) professionals can maintain a single set of rules for remote clients and those that physically connect to an organization’s network. To configure or modify profile settings for a network location, select **Change advanced sharing settings** in the navigation pane of the Network and Sharing Center.

![Screenshot of Windows Defender Security Center, Firewall and network protection.](https://learn.microsoft.com/en-us/training/wwl/manage-defender-windows-client/media/windows-defender-settings-console-bf927211.png)

The first time that you connect a computer to a network, you must select whether you trust the network, which sets appropriate firewall and security settings automatically. When you connect to networks in different locations, you can ensure that your computer is always set to an appropriate security level by choosing a network location.

Windows uses network location awareness to identify networks uniquely to which a computer is connected. Network location awareness collects information from networks, including IP addresses and address data for media access control (MAC) address data from important network components, like routers and gateways, to identify a specific network. If network location awareness recognizes the network as one to which the device has connected previously, network location awareness selects the appropriate network location profile. Otherwise, the user might be prompted to select the network location profile to which to connect the device.

There are three types of network location profiles:

- **Domain networks**. These typically are workplace networks that attach to a domain. A Windows device automatically appears in this network location if it can communicate with a domain controller for the domain to which it is joined. Network discovery is on by default, and you cannot create or join a HomeGroup.
- **Private networks**. These are networks at home or work where you know and trust the people and devices on the network. When you select Home or work (private) networks, this turns on network discovery. Computers on a home network can belong to a HomeGroup.
- **Guest or public networks**. These are networks in public places. This location keeps the computer from being visible to other computers. When you select the Public place network location, Windows turns off network discovery.

You can modify the firewall settings for each type of network location from the main Windows Defender Firewall page. Select **Turn Windows Defender Firewall on or off**, select the network location, and then make your selection. You also can modify the following options:

- Block all incoming connections, including those in the list of allowed programs.
- Notify me when Windows Defender Firewall blocks a new program.

The Public network location blocks certain programs and services from running, which protects a computer from unauthorized access. If you connect to a Public network, and Windows Defender Firewall is on, some programs or services might ask you to allow them to communicate through the firewall so that they can work properly.

### Windows Defender Firewall notifications

You also can display firewall notifications in the taskbar by performing the following steps. In Control Panel, on the Windows Defender Firewall page, in the navigation pane, select **Change notification settings**, and then for each network location, select or clear the **Notify me when Windows Defender Firewall blocks a new app** check box.


Although you still can perform typical end-user configuration in Control Panel through Windows Defender Firewall, you can perform advanced configuration in the Windows Defender Firewall with the Advanced Security snap-in. You can access this snap-in through Control Panel from the Windows Defender Firewall page by selecting **Advanced settings** in the navigation pane. The snap-in provides an interface for configuring Windows Defender Firewall locally, on remote computers, and by using Group Policy.


To configure Windows defender firewall remote use Group  poolicy and locally use the Advanced security snap-in to Windows defender firewall


### Windows Defender Firewall with Advanced Security properties

You can configure basic firewall properties for domain, private, and public network profiles by using the Windows Defender Firewall with Advanced Security Properties dialog box. A firewall profile is a way of grouping settings, including firewall rules and connection security rules. Use the IPsec Settings tab on the Windows Defender Firewall with Advanced Security Properties dialog box to configure the default values for IPsec configuration options.

To access the global profile settings in Windows Defender Firewall with Advanced Security Properties, perform one of the following procedures:

- In the navigation pane, right-click **Windows Defender Firewall with Advanced Security**, and then select **Properties**.
- In the navigation pane, select **Windows Defender Firewall with Advanced Security**, and then in the Overview section, select **Windows Defender Firewall Properties**.
- In the navigation pane, select **Windows Defender Firewall with Advanced Security**, and then in the Actions pane, select **Properties**.

The options that you can configure for each of the three network profiles are:

- **Firewall state**. Turn on or off for each profile.
    
- **Inbound connections**. Configure to block connections that do not match any active firewall rules, block all connections regardless of inbound rule specifications, or allow inbound connections that do not match an active firewall rule.
    
- **Outbound connections**. Configure to allow connections that do not match any active firewall rules or block outbound connections that do not match an active firewall rule.
    
- **Protected network connections**. Configure which network adapters Windows Defender Firewall will protect.
    
- **Settings**. Configure display notifications, unicast responses, local firewall rules, and local connection security rules.
    
- **Logging**. Configure the following logging options:
    
    - **Name**. Use a different name for each network profile’s log file.
        
    - **Size limit (KB)**. The default size is 4,096. Adjust this if necessary when troubleshooting.
        
    - **No logging occurs until you set one or both of following two options to Yes**:
        
        - Log dropped packets
        - Log successful connections

### Windows Defender Firewall with Advanced Security rules

Rules are a collection of criteria that define what traffic you will allow, block, or secure with a firewall. You can configure the following types of rules:

- Inbound
- Outbound
- Connection security rules ![Screenshot of the Windows Defender Firewall with Advanced Security screen](https://learn.microsoft.com/en-us/training/wwl/manage-defender-windows-client/media/windows-defender-advanced-firewall-console-53912b2b.png)

#### Inbound rules

Inbound rules explicitly allow or block traffic that matches the rule’s criteria. For example, you can configure a rule to allow traffic for Remote Desktop from the local network segment through the firewall, but block traffic if the source is a different network segment.

When you first install the Windows operating system, Windows Defender Firewall blocks all unsolicited inbound traffic. To allow a certain type of unsolicited inbound traffic, you must create an inbound rule that describes that traffic. For example, if you want to run a web server, you must create a rule that allows unsolicited inbound network traffic on TCP port 80 for HTTP traffic and TCP port 443 for HTTPS traffic. You can configure the default action that Windows Defender Firewall with Advanced Security takes, which is whether to allow or block connections when an inbound rule does not apply.

#### Outbound rules

Windows Defender Firewall allows all outbound traffic unless a rule blocks it. Outbound rules explicitly allow or deny traffic originating from a computer that matches a rule’s criteria. For example, you can configure a rule to explicitly block outbound traffic to a computer by IP address through the firewall, but allow the same traffic for other computers.

#### Inbound and outbound rule types

There are four different types of inbound and outbound rules:

- **Program rules**. These control connections for a program. Use this type of firewall rule to allow a connection based on the program that is trying to connect. These rules are useful when you are not sure of the port or other required settings, because you only specify the path to the program’s executable (.exe) file.
- **Port rules**. These control connections for a TCP or UDP port. Use this type of firewall rule to allow a connection based on the TCP or UDP port number over which the computer is trying to connect. You specify the protocol and the individual or multiple local ports to which the rule applies.
- **Predefined rules**. These control connections for a Windows-based experience. Use this type of firewall rule to allow a connection by selecting one of the programs or experiences from the list. Network-aware programs that you install typically add their own entries to this list, so that you can enable and disable them as a group.
- **Custom rules**. Configure these as necessary. Use this type of firewall rule to allow a connection based on criteria that other types of firewall rules do not cover.

Consider the scenario in which you want to create and manage tasks on a remote computer by using the Task Scheduler user interface. Before connecting to the remote computer, you must enable the Remote Scheduled Tasks Management firewall exception on the remote computer. You can do this by using the predefined rule type on an inbound rule.

Alternatively, you might want to block all web traffic on the default TCP web server port 80. In this scenario, you create an outbound port rule that blocks the specified port.

#### Connection security rules

Firewall rules and connection security rules are complementary, and both contribute to a defense-in-depth strategy to protect a computer. Connection security rules secure traffic as it crosses a network by using IPsec. Use connection security rules to require authentication or encryption of connections between two computers. Connection security rules specify how and when authentication occurs, but they do not allow connections. To allow a connection, create an inbound or outbound rule. After a connection security rule is in place, you can specify that inbound and outbound rules apply only to specific users or computers.

You can create the following connection security rule types:

- **Isolation rules**. These isolate computers by restricting connections based on authentication criteria, such as domain membership or health status. Isolation rules allow you to implement a server or domain isolation strategy.
- **Authentication exemption rules**. These designate connections that don’t require authentication. You can designate computers by specific IP address, an IP address range, a subnet, or a predefined group, such as a gateway. You typically use this type of rule to grant access to infrastructure computers, such as Active Directory domain controllers, certification authorities (CAs), or Dynamic Host Configuration Protocol (DHCP) servers.
- **Server-to-server rules**. These protect connections between specific computers. When you create this type of rule, you must specify the network endpoints between which you want to protect communications. You then designate requirements and the type of authentication that you want to use, such as the Kerberos version 5 protocol. A scenario in which you might use this rule is if you want to authenticate traffic between a database server and a business-layer computer.
- **Tunnel rules**. These secure communications that travel between two computers by using tunnel mode in IPsec instead of transport mode. Tunnel mode embeds the entire network packet into one that you route between two defined endpoints. For each endpoint, specify a single computer that receives and consumes the sent network traffic, or specify a gateway computer that connects to a private network onto which the received traffic is routed after extracting it from the tunnel.
- **Custom rules**. Configure these as necessary. Custom rules authenticate connections between two endpoints when you cannot set up authentication rules by using the other rule types.

### Monitoring

Windows Defender Firewall uses the monitoring interface to display information about current firewall rules, connection security rules, and security associations (SAs). The Monitoring page displays which profiles are active (domain, private, or public), and the settings for the active profiles.

The Windows Defender Firewall with Advanced Security events also is available in Event Viewer. For example, the ConnectionSecurity operational event log is a resource that you can use to view IPsec-related events. The operational log is always on, and it contains events for connection security rules.