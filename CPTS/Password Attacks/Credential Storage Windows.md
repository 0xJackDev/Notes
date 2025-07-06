
The [Windows client authentication process](https://docs.microsoft.com/en-us/windows-server/security/windows-authentication/credentials-processes-in-windows-authentication) is often more complicated then Linux systems and consists of several different modules that perform the entire logon, retrieval and verification processes. In addition there are many different and complex authentication procedures on the Windows systems such as Kerberos authentication. The  [Local Security Authority](https://learn.microsoft.com/en-us/windows-server/security/credentials-protection-and-management/configuring-additional-lsa-protection) (LSA) is a protected subsystem that authenticates users and logs them into the local computer. In addition the LSA maintains all information about aspects of local security on a computer. It also provides various services for translating between names and security IDs (SIDs)


The security subsystem keeps track of the security policies and accounts that reside on a computer system. In the case of a domain controller, these policies and accounts apply to a domain where the Domain controller is located. These policies and accounts are stored in AD (active directory) in addition, the LSA subsystem provides services for checking access to objects, checking user permissions, and generating monitoring messages.

#### Windows Authentication Process Diagram

![Diagram of Windows Authentication Process showing interactions between WinLogon.exe, LogonUI, lsass.exe, and authentication packages like NTLM and Kerberos.](https://academy.hackthebox.com/storage/modules/147/Auth_process1.png)

Local interactive logon is performed by the interaction between Logon processes ([WinLogon](https://www.microsoftpressstore.com/articles/article.aspx?p=2228450&seqNum=8)), the logon user interface process (LogonUI), the credential providers, LSASS, one or more authentication packages, and SAM or active Directory. Authentication packages,, in this case are the Dynamic-Link libraries (DLLs) that perform authentication checks. For example for a non-domain joined and interactive process, the authentication package Msv1_0.dll is used.

Winlogon is a trusted process responsible for managing security-related user interactions. these include:
- Launching LogonUI to enter passwords at login
- Changing passwords
- Locking and unlocking the workstation

It relies on the credential providers installed on the system to obtain a user's account name or password. Credential providers are COM objects that are located in DLLs

Winlogon is the only process that intercepts login requests from the keyboard sent via a RPC (remote procedure call) message from Win32k.sys. Winlogon immediately launches the LogonUI application at logon to display the user interface for logon. After Winlogon obtains a username and password from the credential providers, it calls LSASS to auth the user before logging in.


## LSASS

Local Security Authority Subsystem Service (LSASS) is a collection of many modules and has access to all authentication processes that can be found in `%SystemRoot%\System32\Lsass.exe`. This service is responsible for the local system security policy, user authentication and sending security audit logs to the event log. In other words it is the vault for Windows-based operating systems and we can find a more detailed illustration of the LSASS architecture https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/cc961760(v=technet.10)?redirectedfrom=MSDN Here.


![Cc961760.DSBG02(en-us,TechNet.10).gif](https://learn.microsoft.com/en-us/previous-versions/windows/it-pro/windows-2000-server/images/cc961760.dsbg02(en-us,technet.10).gif "Cc961760.DSBG02(en-us,TechNet.10).gif")


This is  dogshit diagram just read the docs.



| **Authentication Packages** | **Description**                                                                                                                                                                                                                                                                                                                               |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Lsasrv.dll`                | The LSA Server service both enforces security policies and acts as the security package manager for the LSA. The LSA contains the Negotiate function, which selects either the NTLM or Kerberos protocol after determining which protocol is to be successful. *enforces security policies and acts as the LSA Local security Authority*      |
| `Msv1_0.dll`                | Authentication package for local machine logons that don't require custom authentication. *NTLM authentication protocol*                                                                                                                                                                                                                      |
| `Samsrv.dll`                | The Security Accounts Manager (SAM) stores local security accounts, enforces locally stored policies, and supports APIs. *Stores the Local user accounts and handles auth Locally not via the Domain Controller*                                                                                                                              |
| `Kerberos.dll`              | Security package loaded by the LSA for Kerberos-based authentication on a machine.                                                                                                                                                                                                                                                            |
| `Netlogon.dll`              | Network-based logon service *Net Logon maintains a computers secure channel to a DC (domain controller) and passes the users credentials through a secure channel to the domain controller and returns the domain security identifiers and rights for the user, The net logon services uses DNS to resolve names to the IP addresses of DCs.* |
| `Ntdsa.dll`                 | This library is used to create new records and folders in the Windows registry. *Also support LDAP*                                                                                                                                                                                                                                           |


Each interactive logon session creates a seperate instance of the Winlogon service. The graphical identification and authentication (GINA) is loaded into the process area by Winlogon, which receives and processes the credentials and invokes the authentication interfaces via the LSALogonUser Function. 

## SAM database

https://www.utc.edu/sites/default/files/2021-04/4660-lab6.pdf 

The Security account manager (SAM) is a database file in windows that stores the users passwords. It can be used to authentication local and remote users. SAM uses cryptographic measures to prevent unauthenticated users from accessing the system. User passwords are stored in a hash format in a registry structure as either an LM or a NTLM hash. The file is located in `%SystemRoot%/system32/config/SAM` and is mounted on HKLM/SAM. SYSTEM level permissions are required to view it.


Windows systems can be assigned to either a workgroup or a domain during setup. If the system has been assigned to a workgroup it handles the SAM database locally and stores all existing users in this database. However if the system is joined to a domain, the DC must validate the credentials from the active directory database (ntds.dit) which is stored in `%SystemRoot%\ntds.dit`.


#### Credential Manager

![Diagram of Windows logon process showing interactions between user input, Logon UI, Credential Provider, Winlogon, and Local Security Authority.](https://academy.hackthebox.com/storage/modules/147/authn_credman_credprov.png)


Credential manager is a feature built-in to all windows OS's that allow users to save the credentials they use to access various network resources and websites. Saved credentials are stored based on user profiles in each users Credential Locker. Credentials are encrypted and stored at 

```powershell-session
C:\Users\[Username]\AppData\Local\Microsoft\[Vault/Credentials]\
```

There are various methods to decrypt credentials saved using Credential Manager. We will practice hands-on with some of these methods in this module.


## NTDS

It is very common to come across network environments where windows systems are joined to a windows domain. This is common because it makes it easier for admins to manage all the systems owned by their respective organization (centralized credential management) In those cases the windows systems will send all logon requests to Domain Controllers that belong to the same Active directory forest. Each domain controller hosts a file called NTDS.dit that is kept synced across all Domain controllers with the exception of Read-Only DCs. NTDS.dit is a database file that stored the data in Active Directory not limited to:

- User accounts (username & password hash)
- Group accounts
- Computer accounts
- Group policy objects
- 