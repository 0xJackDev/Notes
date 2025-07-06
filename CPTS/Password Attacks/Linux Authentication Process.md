

Linux-based distributions support various authentication mechanisms. One of the most commonly used in Plug gable Authentication Modules (PAM). The modules responsible for this functionality such as pam_unix.so or pam_unix2.so are typically located in /usr/lib/x86_64-linux-gnu/security/ on Debian based systems. these modules manage user information, authentication, sessions, and password changes. For example when a user changes their password using the passwd command, PAM is invoked which takes the appropriate precautions to handle and store the information accordingly. 

The pam_unix.so module uses standardized api calls from system libraries to update account information. The primary file it reads and writes to are /etc/passwd and /etc/shadow . PAM also includes many other service modules, such as those LDAP, mount operations and kerberos authentication


## PASSWD file

the /etc/passwd file contains information about every user on the system and is readable by all users and services. Each entry in the file corresponds to a single user and consists of seven fields, which store user-related data in a structured format. The fields are separated by colons a typical entry may look like.

```shell-session
htb-student:x:1000:1000:,,,:/home/htb-student:/bin/bash
```

|Field|Value|
|---|---|
|Username|`htb-student`|
|Password|`x`|
|User ID|`1000`|
|Group ID|`1000`|
|[GECOS](https://en.wikipedia.org/wiki/Gecos_field)|`,,,`|
|Home directory|`/home/htb-student`|
|Default shell|`/bin/bash`|


The most relevant field for our purposes is the password field, as it can contain different types of entries. In rare cases (generally on very old systems) this field may hold the actual password hash. However on modern systems however password hashes are stored in the /etc/shadow file. Despite this /etc/passwd file is world read-able. Giving the attackers ability to crack passwords if stored in /etc/passwd


Usually we will find x in the file with the password indicating the password is in /etc/shadow. However it can also be that /etc/passwd is writable
by mistake. This can allow us to remove the password field for root entirely. (change x to 0)

Although the scenarios described are rare, we should still pay attention and watch for potential security gaps, as there are applications that require specific permissions fon entire folders. If the administrator has little experience with Linux (or the applications and their dependencies), they might mistakenly assign write permissions to the `/etc` directory and fail to correct them later.



## Shadow file

Since reading password hash values can put the entire system at risk, the /etc/shadow file was introduced. It has a similar format to /etc/passwd but is solely responsible for password storage and management. It contains all password information for created users. For example if there is no entry in /etc/shadow file for a user listed in /etc/passwd then that user is considered invalid. The /etc/shadow file is also only readable by users with administrative privileges. The format of this file is divided into the following nine fields:

Linux Authentication Process

```shell-session
htb-student:$y$j9T$3QSBB6CbHEu...SNIP...f8Ms:18955:0:99999:7:::
```

| Field             | Value                              |
| ----------------- | ---------------------------------- |
| Username          | `htb-student`                      |
| Password          | `$y$j9T$3QSBB6CbHEu...SNIP...f8Ms` |
| Last change       | `18955`                            |
| Min age           | `0`                                |
| Max age           | `99999`                            |
| Warning period    | `7`                                |
| Inactivity period | `-`                                |
| Expiration date   | `-`                                |
| Reserved field    | `-`                                |
|                   |                                    |
|                   |                                    |

If the password field contains a character such as ! or * the user cannot login using a unix password. However other authentications such as Kerberos or key-based authentication can still be used. The same applies if the password field is empty meaning no password is required for login. This can lead to certain programs denying access to specific functions. The password field also follows a particular format from which we can extract more info

- `$<id>$<salt>$<hashed>`

As we can see here, the hashed passwords are divided into three parts. The `ID` value specifies which cryptographic hash algorithm was used, typically one of the following:

|ID|Cryptographic Hash Algorithm|
|---|---|
|`1`|[MD5](https://en.wikipedia.org/wiki/MD5)|
|`2a`|[Blowfish](https://en.wikipedia.org/wiki/Blowfish_\(cipher\))|
|`5`|[SHA-256](https://en.wikipedia.org/wiki/SHA-2)|
|`6`|[SHA-512](https://en.wikipedia.org/wiki/SHA-2)|
|`sha1`|[SHA1crypt](https://en.wikipedia.org/wiki/SHA-1)|
|`y`|[Yescrypt](https://github.com/openwall/yescrypt)|
|`gy`|[Gost-yescrypt](https://www.openwall.com/lists/yescrypt/2019/06/30/1)|
|`7`|[Scrypt](https://en.wikipedia.org/wiki/Scrypt)|

Many Linux distributions, including Debian, now use `yescrypt` as the default hashing algorithm. On older systems, however, we may still encounter other hashing methods that can potentially be cracked. We'll discuss how the cracking process works shortly.


## Opasswd

The PAM library (pam_unix.so) can prevent users from reusing old passwords. These previous passwords are stored in the /etc/security/opasswd file. Administrator root privileges are required to read this file, assuming its permissions have not been modified manually.

```shell-session
JackTheWizard@htb[/htb]$ sudo cat /etc/security/opasswd

cry0l1t3:1000:2:$1$HjFAfYTG$qNDkF0zJ3v8ylCOrKB0kt0,$1$kcUjWZJX$E9uMSmiQeRh4pAAgzuvkq1
```


Looking at the contents of the file we can see that it contains several entries for the user cry0l1t3, separated by a comma one critical detail to pay attention to is the type of the hash that is used. This is because the MD5 ($1$) algorithm is significantly easier to crack then SHA-512. This is important when identifying old passwords or recognized patterns. As users often reuse similar passwords across multiple services or application. Recognizing these patterns can greatly improve our chances of correctly guessing the password.




## Cracking Linux credentials

Once we have root access on a linux machine we can gather user password hashes and attempt to crack them using various methods to recover plaintext passwords. TO do this we can use a tool called unshadow which is including with john the ripper. It works by combining the passwd and shadow files into a single file for cracking so 

```shell-session
JackTheWizard@htb[/htb]$ sudo cp /etc/passwd /tmp/passwd.bak 
JackTheWizard@htb[/htb]$ sudo cp /etc/shadow /tmp/shadow.bak 
JackTheWizard@htb[/htb]$ unshadow /tmp/passwd.bak /tmp/shadow.bak > /tmp/unshadowed.hashes
```

This "unshadowed" file can now be attacked with either JtR or hashcat.

Linux Authentication Process

```shell-session
JackTheWizard@htb[/htb]$ hashcat -m 1800 -a 0 /tmp/unshadowed.hashes rockyou.txt -o /tmp/unshadowed.cracked
```

**Note:** This is the exact scenario that JtR's `single crack mode` was designed for.


