LSASS stands for Local Security and Authentication subsystem service and is responsible for authentication for both domain and local logons. However the Winlogon process is what determines what logon process to use (local or domain) LSASS Is responsible for verifying the users identity and creating access tokens based on the authentication chosen by win logon

https://learn.microsoft.com/en-us/windows-server/security/windows-authentication/credentials-processes-in-windows-authentication


In addition to getting copies of the SAM database to dump and crack hashes, we will also benefit from targeting LSASS. As discuss in the credential storage part of this module LSASS is a critical service that plays a central role in credential management and the authentication process on windows OS's


![Diagram of Windows authentication process showing interactions between WinLogon.exe, lsass.exe, authentication packages, NTLM, and Kerberos.](https://academy.hackthebox.com/storage/modules/147/lsassexe_diagram.png)


Upon initial logon LSASS will 

- Cache credentials locally in memory
- Create access tokens
- enforce security policies
- and Write to windows Security log

Lets cover some of the techniques and tools we can use to dump LSASS memory


## Dumping LSASS Process memory

Similar to the process of attacking the SAM database, with LSASS it would be wise for us first to create a copy of the contents of LSASS process memory via the generation of a memory dump. Creating a dump file lets us extract credentials offline using our attack host. Keep in mind conduction attacks offline gives us more flexibility. There are countless ways to create a memory dump



## Task Manager Memory dump method

With access to a interactive graphical session with the target we can use task manager to create a memory dump

requires us to:

![Task Manager showing Local Security Authority Process with right-click menu open, highlighting 'Create dump file' option, and lsass.DMP file in search results.](https://academy.hackthebox.com/storage/modules/147/taskmanagerdump.png)

`Open Task Manager` > `Select the Processes tab` > `Find & right click the Local Security Authority Process` > `Select Create dump file`

A file called `lsass.DMP` is created and saved in:

Attacking LSASS

```cmd-session
C:\Users\loggedonusersdirectory\AppData\Local\Temp
```



## Rundll32.exe and Comsvcs.dll Method

The task manager method requires us to have GUI access to a target. We can use another method to dump LSASS process memory through a CLI utility called rundll32.exe. This is way faster then task manager and more flexible because we may gain a shell session with a windows host with only access to CLI. It is important to note that most modern anti-viruses pick up this method as malicious activity


Before issuing the command to create the dump we must first find out the PID of lsass.exe 


#### Finding LSASS PID in cmd

From cmd, we can issue the command `tasklist /svc` and find lsass.exe and its process ID in the PID field.

Attacking LSASS

```cmd-session
C:\Windows\system32> tasklist /svc
```


#### Finding LSASS PID in PowerShell

From PowerShell, we can issue the command `Get-Process lsass` and see the process ID in the `Id` field.

Attacking LSASS

```powershell-session
PS C:\Windows\system32> Get-Process lsass
```


#### Creating lsass.dmp using PowerShell

With an elevated PowerShell session, we can issue the following command to create the dump file:

Attacking LSASS

```powershell-session
PS C:\Windows\system32> rundll32 C:\windows\system32\comsvcs.dll, MiniDump 672 C:\lsass.dmp full
```

In this scenerario 672 is the PID 


with this command we are running rundll32.exe to call an exported function of comsvcs.dll which also calls the MiniDumpWriteDump (MiniDump) to dump the LSASS process memory into the directory C:\lsass.dmp . This is not FUD (fully undetected)


If we manage to run this command and generate the `lsass.dmp` file, we can proceed to transfer the file onto our attack box to attempt to extract any credentials that may have been stored in LSASS process memory.



## ## Using Pypykatz to Extract Credentials

Once we have the .dmp file or dump file on our attack host we can use  https://github.com/skelsec/pypykatz to extract credentials from the .dmp file. Pypykatz is mimikatz written in python so we can use it on linux-based hosts. At this time mimikatz only runs on windows. Mimikatz only runs on Windows systems, so to use it, we would either need to use a Windows attack host or we would need to run Mimikatz directly on the target, which is not an ideal scenario. This makes Pypykatz an appealing alternative because all we need is a copy of the dump file, and we can run it offline from our Linux-based attack host.

Recall that LSASS stores credentials that have active logon sessions on Windows systems. When we dumped LSASS process memory into the file, we essentially took a "snapshot" of what was in memory at that point in time. If there were any active logon sessions, the credentials used to establish them will be present. Let's run Pypykatz against the dump file and find out.


## #### Running Pypykatz


the command initates the use of pypykatz to parse the secrets hidden in the LSASS process memory dump. We use LSA in the command because LSASS is a subsystem of LSA or (Local Security authority) then we specify the data source as the mini dump file proceeded by the path to the dump file stored on our attack host.

Pypykatz parses the dump file and outputs the findings:

Attacking LSASS

```shell-session
JackTheWizard@htb[/htb]$ pypykatz lsa minidump /home/peter/Documents/lsass.dmp 
```



It outputs several things. lets take a look

## MSV (Microsoft security validation )
its referred to as its module name MSV1_0.dll

```shell-session
sid S-1-5-21-4019466498-1700476312-3544718034-1001
luid 1354633
	== MSV ==
		Username: bob
		Domain: DESKTOP-33E7O54
		LM: NA
		NT: 64f12cddaa88057e06a81b54e73b949b
		SHA1: cba4e545b7ec918129725154b29f055e4cd5aea8
		DPAPI: NA
```

MSV is a authentication package in Windows that LSA calls to validate logon attempts against the SAM database. Pypykatz extract the SID (security identifier), Username and Domain, and even the NT and SHA1 Password hashes associated with the bob users account logon stored in LSASS process memory. This will be useful in the final stage of our attack.
This will only have credentials that are already existent in the SAM database.




## WDIGEST

```shell-session
	== WDIGEST [14ab89]==
		username bob
		domainname DESKTOP-33E7O54
		password None
		password (hex)
```


This is an older authentication protocol enabled in anything before windows 10. LSASS caches credentials used by WDIGEST in clear-text. This means if we find ourselves targeting a Windows system with WDIGEST enabled, we will most likely see a password in clear-text. Modern Windows operating systems have WDIGEST disabled by default. Additionally, it is essential to note that Microsoft released a security update for systems affected by this issue with WDIGEST. We can study the details of that security update [here](https://msrc-blog.microsoft.com/2014/06/05/an-overview-of-kb2871997/). prob wont ever see shit here tbh






#### Kerberos


```shell-session
	== Kerberos ==
		Username: bob
		Domain: DESKTOP-33E7O54
```

Kerberos is a network authentication protocol used by active directory in Windows Domain environments. Domain users accounts are granted tickets upon authentication with active directory. This ticket is used to allow the user to access shared resources on the network they have been granted access to without needing to type their credentials each time. LSASS caches passwords, ekeys, tickets and pins associated with Kerberos. It is possible to extract these from LSASS process memory and use them to access other systems joined to the same domain.




## DPAPI 
```shell-session
== DPAPI [14ab89]==
		luid 1354633
		key_guid 3e1d1091-b792-45df-ab8e-c66af044d69b
		masterkey e8bc2faf77e7bd1891c0e49f0dea9d447a491107ef5b25b9929071f68db5b0d55bf05df5a474d9bd94d98be4b4ddb690e6d8307a86be6f81be0d554f195fba92
		sha1_masterkey 52e758b6120389898f7fae553ac8172b43221605
```

The Data protection application programming interface or DPAPI is a set of APIs in windows used to encrypt and decrypt DPAPI data blobs on a per-user basis for windows OS features and third party applications. Here are a few use cases 

|Applications|Use of DPAPI|
|---|---|
|`Internet Explorer`|Password form auto-completion data (username and password for saved sites).|
|`Google Chrome`|Password form auto-completion data (username and password for saved sites).|
|`Outlook`|Passwords for email accounts.|
|`Remote Desktop Connection`|Saved credentials for connections to remote machines.|
|`Credential Manager`|Saved credentials for accessing shared resources, joining Wireless networks, VPNs and more.|


This is how I extracted the master key for brave browser I believe to decrypt and get those passwords. This masterkey can then be used to decrypt the secrets associated with each of the applications using DPAPI and result in the capturing of credentials for various accounts. DPAPI attack techniques are covered in greater detail in the [Windows Privilege Escalation](https://academy.hackthebox.com/module/details/67) module.



## Cracking 