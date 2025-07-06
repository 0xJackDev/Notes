
Hunting for credentials is one of the first steps once we have access to the system. These low-hanging fruits can give us elevated privileges within seconds or minutes. Among other things this is part of the local privilege esclatation process that we will cover here. However it is important to note here that we are far from covering all possible situations and therefore focus on the different approaches.

We can imagine we have successfully gained access to a system via  vulnerable web application and have therefor obtained a reverse shell, for example. Therefore to esclate our privledges most efficiently we can search for passwords or even whole credentials that we can use to login to our target. There are several sources that can provide us with credentials, we can put them into four categories.

- `Files` including configs, databases, notes, scripts, source code, cronjobs, and SSH keys
- `History` including logs, and command-line history
- `Memory` including cache, and in-memory processing
- `Key-rings` such as browser stored credentials


Enumerating all those categories will al low us to increase the probability of successfully finding out - with some ease - credentials of existing users of the system. There are countless different situations in which we will always see different results. Therefor we should adapt our approach to the circumstances of the environment and keep the big picture in mind. Above all it is cruicial to keep  in mind how the system works, its focuses, what purpose it exists for, what role it plays in the business logic and overall network. For example suppose it is a isolated database server. In that case we will not find normal users there since it is a sensitive information interface in the management of data to which only few people are granted access/


## Files

One core principle of linux is that everything is a file. Therefore it is crucial to keep this concept in mind and search, find and filter the appropriate files according to our requirements we should look for, find and inspect several categories of files one by one. These categories are the following

- Configuration files
- Databases
- Notes
- Scripts
- Cronjobs
- SSH keys
Configuration files are the functionality of services on Linux distributions. Often they even contain credentials that we will be able to read. Their insight also allows us to understand how the service works and its requirements precisely. usually the configuration files are marked with the  following three file exxtensions (.config, .conf,  .cnf). However these configuration files or the associated extension files can be renamed which means that these file extensions are not necessarily required. Furthermore even when recompiling a service the requiring filename for the basic configuration cab be changed which would result in the same effect.


You can use this to find config files

```shell-session
for l in $(echo ".conf .config .cnf");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "lib\|fonts\|share\|core" ;done
```



Optionally we can save the result ot a text file. In this example we search for three words (user,pass, password)
```shell-session
for i in $(find / -name *.cnf 2>/dev/null | grep -v "doc\|lib");do echo -e "\nFile: " $i; grep "user\|password\|pass" $i 2>/dev/null | grep -v "\#";done
```


## Searching for databases

```shell-session
for l in $(echo ".sql .db .*db .db*");do echo -e "\nDB File extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc\|lib\|headers\|share\|man";done
```


#### Searching for notes

```shell-session
find /home/* -type f -name "*.txt" -o ! -name "*.*"
```


## Searching for scripts

```shell-session
for l in $(echo ".py .pyc .pl .go .jar .c .sh");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc\|lib\|headers\|share";done
```

#### Enumerating cronjobs

Cronjobs are independent execution of commands, programs, scripts. These are divided into the system-wide area (`/etc/crontab`) and user-dependent executions. Some applications and scripts require credentials to run and are therefore incorrectly entered in the cronjobs. Furthermore, there are the areas that are divided into different time ranges (`/etc/cron.daily`, `/etc/cron.hourly`, `/etc/cron.monthly`, `/etc/cron.weekly`). The scripts and files used by `cron` can also be found in `/etc/cron.d/` for Debian-based distributions.


```shell-session
cat /etc/crontab 
```



#### Enumerating history files

All history files provide crucial information about the current and past/historical course of processes. We are interested in the files that store users' command history and the logs that store information about system processes.

In the history of the commands entered on Linux distributions that use Bash as a standard shell, we find the associated files in `.bash_history`. Nevertheless, other files like `.bashrc` or `.bash_profile` can contain important information.

```shell-session
tail -n5 /home/*/.bash*
```



#### Enumerating log files

```shell-session
for i in $(ls /var/log/* 2>/dev/null);do GREP=$(grep "accepted\|session opened\|session closed\|failure\|failed\|ssh\|password changed\|new user\|delete user\|sudo\|COMMAND\=\|logs" $i 2>/dev/null); if [[ $GREP ]];then echo -e "\n#### Log file: " $i; grep "accepted\|session opened\|session closed\|failure\|failed\|ssh\|password changed\|new user\|delete user\|sudo\|COMMAND\=\|logs" $i 2>/dev/null;fi;done
```

An essential concept of Linux systems is log files that are stored in text files. Many programs, especially all services and the system itself, write such files. In them, we find system errors, detect problems regarding services or follow what the system is doing in the background. The entirety of log files can be divided into four categories:

- Application logs
- Event logs
- Service logs
- System logs

Many different logs exist on the system. These can vary depending on the applications installed, but here are some of the most important ones:

|**File**|**Description**|
|---|---|
|`/var/log/messages`|Generic system activity logs.|
|`/var/log/syslog`|Generic system activity logs.|
|`/var/log/auth.log`|(Debian) All authentication related logs.|
|`/var/log/secure`|(RedHat/CentOS) All authentication related logs.|
|`/var/log/boot.log`|Booting information.|
|`/var/log/dmesg`|Hardware and drivers related information and logs.|
|`/var/log/kern.log`|Kernel related warnings, errors and logs.|
|`/var/log/faillog`|Failed login attempts.|
|`/var/log/cron`|Information related to cron jobs.|
|`/var/log/mail.log`|All mail server related logs.|
|`/var/log/httpd`|All Apache related logs.|
|`/var/log/mysqld.log`|All MySQL server related logs.|


## Memory and cache

#### Mimipenguin

Many applications and processes work with credentials needed for authentication and store them either in memory or in files so that they can be reused. For example, it may be the system-required credentials for the logged-in users. Another example is the credentials stored in the browsers, which can also be read. In order to retrieve this type of information from Linux distributions, there is a tool called [mimipenguin](https://github.com/huntergregal/mimipenguin) that makes the whole process easier. However, this tool requires administrator/root permissions.

Credential Hunting in Linux

```shell-session
JackTheWizard@htb[/htb]$ sudo python3 mimipenguin.py

[SYSTEM - GNOME]	cry0l1t3:WLpAEXFa0SbqOHY
```


#### LaZagne

An even more powerful tool we can use that was mentioned earlier in the Credential Hunting in Windows section is `LaZagne`. This tool allows us to access far more resources and extract the credentials. The passwords and hashes we can obtain come from the following sources but are not limited to:


For example, `Keyrings` are used for secure storage and management of passwords on Linux distributions. Passwords are stored encrypted and protected with a master password. It is an OS-based password manager, which we will discuss later in another section. This way, we do not need to remember every single password and can save repeated password entries.

Credential Hunting in Linux

```shell-session
JackTheWizard@htb[/htb]$ sudo python2.7 laZagne.py all
```



#### Browser credentials

The tool [Firefox Decrypt](https://github.com/unode/firefox_decrypt) is excellent for decrypting these credentials, and is updated regularly. It requires Python 3.9 to run the latest version. Otherwise, `Firefox Decrypt 0.7.0` with Python 2 must be used.

Credential Hunting in Linux

```shell-session
JackTheWizard@htb[/htb]$ python3.9 firefox_decrypt.py
```



Browsers store the passwords saved by the user in an encrypted form locally on the system to be reused. For example, the `Mozilla Firefox` browser stores the credentials encrypted in a hidden folder for the respective user. These often include the associated field names, URLs, and other valuable information.

For example, when we store credentials for a web page in the Firefox browser, they are encrypted and stored in `logins.json` on the system. However, this does not mean that they are safe there. Many employees store such login data in their browser without suspecting that it can easily be decrypted and used against the company.

Credential Hunting in Linux

```shell-session
[!bash]$ ls -l .mozilla/firefox/ | grep default 

drwx------ 11 cry0l1t3 cry0l1t3 4096 Jan 28 16:02 1bplpd86.default-release
drwx------  2 cry0l1t3 cry0l1t3 4096 Jan 28 13:30 lfx3lvhb.default
```

Credential Hunting in Linux

```shell-session
JackTheWizard@htb[/htb]$ cat .mozilla/firefox/1bplpd86.default-release/logins.json | jq .
```


Alternatively, `LaZagne` can also return results if the user has used the supported browser.



to do the challenge just zip lazagne. transfer it over then unzip it and then run the linux python file

[+] Password found !!!
URL: https://dev.inlanefreight.com
Login: will@inlanefreight.htb
Password: TUqr7QfLTLhruhVbCP


