

As discussed previously, the need for the ability to work remotely and access organizational resources is becoming commonplace today. While tools like OneDrive help with managing user files and solutions like SharePoint online facilitate access to resources in the cloud, some resources can only be accessed while on the corporate network. In these scenarios, a virtual private network (VPN) connection must be established.


#### Objectives

After this lesson, you should be able to:

- Describe how you can access corporate resources
- Describe VPN types and configuration
- Describe Always On VPN
- Describe how to configure Always On VPN


In Windows Server 1016 or later Windows 10 or later Clients Can be Setup as a Remote Server Access Role That can be configured as a server that terminates and routes VPN connections established from the internet or other external networks. In Windows environments, VPN connections were mostly established on-demand, and based on PPTP, L2TP or SSTP protocol. However, you can also choose other ways to access internal resources, from the outside, or you can choose to publish internal resources on external networks such as the internet.



In Windows Server 2016 and later, you can find several services that you can use to make internal resources accessible from the outside. You can use Work Folders, to synchronize content from specific folders on Windows machines with file servers, even when your client is located outside the internal network. If you want to publish internal apps and services to the internet, by using specific web-based protocols, you can use the Web Application Proxy service in Windows Server.


To create seamless connections between internal servers and clients located outside, Microsoft originally introduced the DirectAccess technology. This technology provided the ability not just to access internal resources without manually establishing a VPN connection, but also to manage external clients with management tools such as Microsoft Configuration Manager and Group Policy, even when they aren't in the internal network. This technology evolved to Always On VPN, available in Windows Server 2016 and later. Most technologies for remote access or publishing of internal resources are based on the Remote Access server role in Windows Server.



The Remote Access server role is a logical grouping of the following related network access technologies: Remote Access Service (RAS), Routing, and Web Application Proxy. These technologies are the role services of the Remote Access server role. When you install the Remote Access server role with the Add Roles and Features Wizard or Windows PowerShell, you can install one or more of these three role services.


Do not attempt to deploy Remote Access on a virtual machine (VM) in Microsoft Azure. Using Remote Access in Microsoft Azure is not supported. You cannot use Remote Access in an Azure VM to deploy VPN, DirectAccess, or any other Remote Access feature in Windows Server 2016 or earlier versions of Windows Server.

When you install the DirectAccess and VPN (RAS) role services, you're deploying the Remote Access Service Gateway (RAS Gateway). You can deploy the RAS Gateway as a single tenant RAS Gateway virtual private network (VPN) server, a multitenant RAS Gateway VPN server, and as a DirectAccess server.

- **RAS Gateway - single tenant**. By using RAS Gateway, you can deploy VPN connections to provide end users with remote access to your organization's network and resources. If your clients are running Windows 10 Pro, Enterprise or Education or later, you can deploy Always On VPN, which maintains a persistent connection between clients and your organization network whenever remote computers are connected to the internet. With RAS Gateway, you can also create a site-to-site VPN connection between two servers at different locations, such as between your primary office and a branch office, and use Network Address Translation (NAT) so that users inside the network can access external resources, such as the internet. In addition, RAS Gateway supports Border Gateway Protocol (BGP), which provides dynamic routing services when your remote office locations also have edge gateways that support BGP.
- **RAS Gateway - multitenant**. You can deploy RAS Gateway as a multitenant, software-based edge gateway and router when you're using Hyper-V Network Virtualization or you have VM networks deployed with virtual Local Area Networks (VLANs). With the RAS Gateway, Cloud Service Providers (CSPs) and enterprises can enable datacenter and cloud network traffic routing between virtual and physical networks, including the internet. With the RAS Gateway, your tenants can use point-to-site VPN connections to access their VM network resources in the datacenter from anywhere. You can also provide tenants with site-to-site VPN connections between their remote sites and your CSP datacenter. In addition, you can configure the RAS Gateway with BGP for dynamic routing, and you can enable Network Address Translation (NAT) to provide internet access for VMs on VM networks.
- **Always On VPN**. Always On VPN enables remote users to securely access shared resources, intranet websites, and applications on an internal network without connecting to a VPN.



RAS Gateway Multi tenant - is Virtualization

RAS Gateway Single tenant 
 By using RAS Gateway, you can deploy VPN connections to provide end users with remote access to your organization's network and resources. If your clients are running Windows 10 Pro, Enterprise or Education or later, you can deploy Always On VPN, which maintains a persistent connection between clients and your organization network whenever remote computers are connected to the internet.
- **Always On VPN**. Always On VPN enables remote users to securely access shared resources, intranet websites, and applications on an internal network without connecting to a VPN.


# Explore VPN types and configuration

Completed100 XP

- 3 minutes

Virtual private networks (VPNs) are point-to-point connections across a private or public network, such as the internet. A VPN client uses special TCP/IP or UDP-based protocols, called tunneling protocols, to make a virtual call to a virtual port on a VPN server. In a typical VPN deployment, a client initiates a virtual point-to-point connection to a remote access server over the internet. The remote access server answers the call, authenticates the caller, and transfers data between the VPN client and the organization’s private network.

There are many options for VPN clients. In Windows, the built-in plug-in and the Universal Windows Platform (UWP) VPN plug-in platform are built on top of the Windows VPN platform.

![Diagram of VPN connection types.](https://learn.microsoft.com/en-us/training/wwl/organizational-access/media/windows-vpn-platform-ffcf080a.png)

### Built-in VPN client

Windows provides a built-in VPN client software that you can configure to establish various types of VPN connections. VPN connections can use different tunneling protocols. You should configure same tunneling protocol on both VPN server and VPN client side. In Windows, following tunneling protocols are supported:

- Internet Key Exchange version 2 (IKEv2) - Configure the IPsec/IKE tunnel cryptographic properties using the Cryptography Suite setting in the VPNv2 Configuration Service Provider (CSP).
- L2TP - L2TP with pre-shared key (PSK) authentication can be configured using the L2tpPsk setting in the VPNv2 CSP.
- PPTP - Point-to-Point Tunneling Protocol.
- SSTP - SSTP is supported for Windows desktop editions only. SSTP can't be configured using mobile device management (MDM), but it’s one of the protocols attempted in the Automatic option.

If you don’t know which tunneling protocol to use, you can also choose automatic configuration of VPN client. The Automatic option means that the device will try each of the built-in tunneling protocols until one succeeds. It will attempt from most secure to least secure.

### Universal Windows Platform VPN plug-in

The Universal Windows Platform (UWP) VPN plug-ins were introduced in Windows 10, although there were originally separate versions available for the Windows 8.1 Mobile and Windows 8.1 PC platforms. Using the UWP platform, third-party VPN providers can create app-containerized plug-ins using WinRT APIs, eliminating the complexity and problems often associated with writing to system-level drivers.

There are many Universal Windows Platform VPN applications, such as Pulse Secure, Cisco AnyConnect, F5 Access, SonicWall Mobile Connect, and Check Point Capsule. If you want to use a UWP VPN plug-in, work with your vendor for any custom settings needed to configure your VPN solution.




Types of VPN Technology for Normal Non ALways on Is UWP or Universial Windows Platform VPN plug-in 
and The Built-in Windows Vpn Client as well.


# Explore Always On VPN

Completed100 XP

- 3 minutes

Always On VPN is a technology introduced in Windows 10 that allows users to stay connected to their internal network even when they're outside company premises or, in general, whenever they're connected to the internet. Unlike traditional VPN connection, which requires a user to manually initiate when they want to connect to a company's network, Always On VPN does this automatically, even before the user signs in, if configured that way. Also, when internet links fail, it reconnects automatically when the internet connection is restored without user action. With this technology, users don't need to be concerned about initiating a VPN connection to access a resource. When Always On VPN infrastructure is set up, users have seamless access to external and internal resources despite their physical location.



Always On VPN is a direct successor of DirectAccess technology

You can initiate an Always On VPN connection even from Windows Home edition devices. Always On VPN has mitigated most of the limitations of earlier VPN solutions and expanded the VPN functionality beyond the capabilities of DirectAccess or traditional VPN.

Always On VPN can work on both domain and non-domain joined devices. It supports both user and device authentication and uses traditional remote access VPN protocols such as IKEv2, SSTP, and L2TP/IPsec, as well as IPv4 and IPv6. As both managed and un-managed devices are supported to initiate Always On VPN connections, you can use conditional access and device compliance policies with Always On VPN to maintain acceptable level of security. You can also use new methods of authentication, such as Windows Hello for Business and multifactor authentication. If you want to enable access to only some of the internal network, you can implement traffic filters and allow external access only to selected resources in the internal network.



Always On VPN is exclusively a Windows 11 and Windows 10 feature–devices using other platforms would need to use traditional client VPN solutions. Also, you can't use Active Directory Domain Services (AD DS) or Group Policy to deploy and manage this feature. You need to use Configuration Manager, Microsoft Intune, or PowerShell. Windows Server 2022 and later, with the Routing and Remote Access role installed supports Always On VPN technology. However, other network devices (from vendors such as Cisco, Juniper, Palo Alto, and others) that can terminate VPN connections are also supported.



Have to Use Intune or Powershell or Configuration manager to Deploy Always On vpn and its only for Windows 11 and 10 devices 




# Deploy Always On VPN

Completed100 XP

- 3 minutes

You most likely have the technologies you can use to deploy Always On VPN. Other than your DC/DNS servers, the Always On VPN deployment requires an NPS (RADIUS) server, a Certification Authority (CA) server, and a Remote Access (Routing/VPN) server. Once the infrastructure is set up, you must enroll clients, and then connect the clients to your on-premises securely through several network changes.

When preparing for Always On VPN deployment, you should ensure that you have the following components in place:

- Active Directory domain infrastructure, including one or more Domain Name System (DNS) servers. Both internal and external Domain Name System (DNS) zones are required, which assumes that the internal zone is a delegated subdomain of the external zone (for example, corp.contoso.com and contoso.com).
- 
- Active Directory-based public key infrastructure (PKI) and Microsoft Entra Certificate Services (AD CS).
- Physical server, existing or new, to install Network Policy Server (NPS). If you already have NPS servers on your network, you can modify an existing NPS server configuration rather than add a new server.
- Remote Access as a RAS Gateway VPN server with features supporting IKEv2 VPN connections and LAN routing.
- 
- Perimeter network that includes two firewalls. Ensure that your firewalls allow the traffic necessary for both VPN and RADIUS communications to function properly.
- Physical server or VM on your perimeter network with two physical Ethernet network adapters to install Remote Access as a RAS Gateway VPN server. VMs require virtual LAN (VLAN) for the host.
- Membership in Administrators, or equivalent, is the minimum required.
- Management platform of your choice for deploying the Always On VPN configuration because the CSP isn't vendor-specific.

The following illustration shows the infrastructure required to deploy Always On VPN.

![Diagram showing the Always On VPN infrastructure.](https://learn.microsoft.com/en-us/training/wwl/organizational-access/media/vpn-perimeter-diagram-97027b4d.png)