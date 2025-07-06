

For this one I do a nmap scan

```
[haxor@skid pen]$ nmap -sC -sV 10.129.18.157
Starting Nmap 7.95 ( https://nmap.org ) at 2025-02-22 02:56 UTC
Stats: 0:00:01 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Connect Scan Timing: About 2.95% done; ETC: 02:57 (0:00:33 remaining)
Stats: 0:01:14 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 97.96% done; ETC: 02:57 (0:00:00 remaining)
Stats: 0:01:14 elapsed; 0 hosts completed (1 up), 1 undergoing Script Scan
NSE Timing: About 97.96% done; ETC: 02:57 (0:00:00 remaining)
Nmap scan report for 10.129.18.157
Host is up (0.044s latency).
Not shown: 979 closed tcp ports (conn-refused)
PORT      STATE    SERVICE        VERSION
43/tcp    filtered whois
106/tcp   filtered pop3pw
111/tcp   open     rpcbind?
| rpcinfo:
|   program version    port/proto  service
|   100003  2,3         2049/udp   nfs
|   100003  2,3         2049/udp6  nfs
|   100003  2,3,4       2049/tcp   nfs
|_  100003  2,3,4       2049/tcp6  nfs
135/tcp   open     msrpc          Microsoft Windows RPC
139/tcp   open     netbios-ssn    Microsoft Windows netbios-ssn
445/tcp   open     microsoft-ds?
524/tcp   filtered ncp
631/tcp   filtered ipp
1047/tcp  filtered neod1
1069/tcp  filtered cognex-insight
1076/tcp  filtered sns_credit
2048/tcp  filtered dls-monitor
2049/tcp  open     nfs            2-4 (RPC #100003)
2121/tcp  filtered ccproxy-ftp
2718/tcp  filtered pn-requester2
3372/tcp  filtered msdtc
3389/tcp  open     ms-wbt-server  Microsoft Terminal Services
|_ssl-date: 2025-02-22T02:58:03+00:00; 0s from scanner time.
| ssl-cert: Subject: commonName=WINMEDIUM
| Not valid before: 2025-02-21T01:56:09
|_Not valid after:  2025-08-23T01:56:09
| rdp-ntlm-info:
|   Target_Name: WINMEDIUM
|   NetBIOS_Domain_Name: WINMEDIUM
|   NetBIOS_Computer_Name: WINMEDIUM
|   DNS_Domain_Name: WINMEDIUM
|   DNS_Computer_Name: WINMEDIUM
|   Product_Version: 10.0.17763
|_  System_Time: 2025-02-22T02:57:53+00:00
5985/tcp  open     http           Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
8300/tcp  filtered tmi
9943/tcp  filtered unknown
32783/tcp filtered unknown
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-time:
|   date: 2025-02-22T02:57:55
|_  start_date: N/A
| smb2-security-mode:
|   3:1:1:
|_    Message signing enabled but not required


```


I see NFS and smb. So thats what i try first

so I enumurate the NFS shares with

showmount -e 10.129.18.157

Which returns a /TechSupport Mount

https://medium.com/@karan_shergill/network-file-system-nfs-enumeration-exploitation-14c154a4d2c1

Heres a useful article

ALSO PLEASE KEEP IN MIND IF YOU GET ANY ERRORS YOU MUST USE SUDO 

sudo mkdir /tmp/mount3 && sudo mount 10.129.18.157:/TechSupport /tmp/mount3


so run this.

And for some reason i had to change to a root shell in order to into this mounted share.


And i see a large listing of tickets.


So among this i search for the string pass in all the files recursivley


[root@skid mount3]# grep -r "pass" .
./ticket4238791283782.txt: 6    password="lol123!mD"
./ticket4238791283782.txt:16    userpass {
[root@skid mount3]#


 1smtp {
 2    host=smtp.web.dev.inlanefreight.htb
 3    #port=25
 4    ssl=true
 5    user="alex"
 6    password="lol123!mD"
 7    from="alex.g@web.dev.inlanefreight.htb"
 8}
 9
Investigating the file more I find this.
pop3pw
remember their pop3pw server on port 106


I cant connect so lets maybe just try evil-winrm

No. That doesnt work. But SMB does



smbclient -L 10.129.18.157 -U alex%lol123\!mD


(1/1) Arming ConditionNeedsUpdate...
[root@skid mount3]# smbclient -L 10.129.18.157 -U alex%lol123\!mD
Can't load /etc/samba/smb.conf - run testparm to debug it

	Sharename       Type      Comment
	---------       ----      -------
	ADMIN$          Disk      Remote Admin
	C$              Disk      Default share
	devshare        Disk
	IPC$            IPC       Remote IPC
	Users           Disk
tstream_smbXcli_np_destructor: cli_close failed on pipe srvsvc. Error was NT_STATUS_IO_TIMEOUT
SMB1 disabled -- no workgroup available
[root@skid mount3]#


Cool beans we connect to the devshare share and then get a file named important.txt

sa:87N1ns@slls83


```
rpcclient -U alex 10.129.18.157 # when prompted, enter: lol123!mD
```


/usr/bin/smbmap.py

```
SMBMap - Samba Share Enumerator v1.10.4 | Shawn Evans - ShawnDEvans@gmail.com<mailto:ShawnDEvans@gmail.com>
                     https://github.com/ShawnDEvans/smbmap

[*] Detected 1 hosts serving SMB
[*] Established 1 SMB connections(s) and 1 authenticated session(s)

[+] IP: 10.129.18.157:445	Name: 10.129.18.157       	Status: Authenticated
	Disk                                                  	Permissions	Comment
	----                                                  	-----------	-------
	ADMIN$                                            	NO ACCESS	Remote Admin
	C$                                                	NO ACCESS	Default share
	devshare                                          	READ, WRITE	
	IPC$                                              	READ ONLY	Remote IPC
	Users                                             	READ ONLY	
[*] Closed 1 connections
(venv) [haxor@skid pen]$
```

/usr/bin/smbmap.py -H 10.129.18.157 -u alex -p 'lol123!mD'

Inside of of the Users share I find the 

This is one of the ones where I feel a little dumb

xfreerdp /u:alex /p:'lol123!rD' /v:10.129.17.105






Now there is a SQL server I can launch. Guess what I got the password!!

*Make sure you launch as admin with these credentials*
*Highly suggest using pwn box*

sa:87N1ns@slls83
87N1ns@slls83


xfreerdp /u:alex /p:'lol123!mD' /v:10.129.82.230



Ok logging into this confused be just since you logged in as admin you can just login to WinMedium




In the final stage of the challenge, I focused on the SQL Server to extract the HTB user’s password. I connected to the SQL Server instance and switched to the “accounts” database, where I knew application credentials were stored. After listing the tables, I found one named **devsacc** that contained user information—specifically columns for id, name, and password. I then ran a query:
```

SELECT id, name, password
FROM devsacc
WHERE name = 'HTB';

```

And boom! 