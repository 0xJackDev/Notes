
MySQL is an open source SQL relational database management system developed by Oracle. the database is stored with a .sql file extension 


## MYSQL clients
The Mysql client can retrieve and edit the data using SQL to the database engine. One of the best examples of Database is the CMS wordpress. WordPress stores all created posts usernames and password in their own database. 



## MySQL databases

MySQL is suited for dynamic websites where efficient syntax and high speed are essential. It is often combined with a LEMP or a LAMP stack. 


## Footprinting the Service

There are many reasons why a MySQL server could be accessed from an external network. Nevertheless, it is far from being one of the best practices, and we can always find databases that we can reach. Often, these settings were only meant to be temporary but were forgotten by the administrators. This server setup could also be used as a workaround due to a technical problem. Usually, the MySQL server runs on `TCP port 3306`, and we can scan this port with `Nmap` to get more detailed information.

#### Scanning MySQL Server

MySQL

```shell-session
JackTheWizard@htb[/htb]$ sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*
```



I use this command above to 
10.129.58.255


After connecting to their mysql server with

mysql -u robin -probin -h 10.129.58.255 --ssl-verify-server-cert=0

SELECT email FROM myTable WHERE name = 'Otto Lang';
