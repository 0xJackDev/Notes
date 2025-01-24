
As A network admin you will work with UDP and TCP port number and u needa know important


Telnet - Telecommunication  Network
Tcp
Port 23 
If you need to get a console screen from a remote device 
Console access Unencrypted
BAD CHOICE NEVER USE



SSH - Standard Secure Shell
TCP
port 22
This is an encrypted communication link giving you a shell into the system
Looks and acts the same as Telnet but encrypted





DNS Domain Name System
Converts Names Into Ip addresses
This uses 
UDP 
Port 53 
Large transfers may use TCP port 53 though
These are critical resources theres usually multiple DNS servers in production



SMTP - Simple Mail Transfer Protocol
TCP
- This is Server To server email transfer
- If you are using SMTP unencrypted you are using port 25 With TCP
- If you are Sending SMTP with TLS encryption you are using TCP port 587
Also used to send mail from a device to a mail server, other protocols are used to receive email





POP3 / IMAP

This is a easy way to receive emails from a email server and authenticate.


POP3 stands for Post office Protocol version 3:
TCP 
Port 110 used for Plaintext/Unencrypted
Port 995 used for POP3 over TLS 
this is basic mail transfer functionality


IMAP4 - Internet Message access Protocol V4 
TCP
Port 143 for plaintext
Port 993 for IMAP over TLS,
This includes management of email inboxes from multiple clients and it gives us more options for example if we delete email on one device it deletes the email on all. 




There are many ways to transfer a file from one device to another across a network, One of the more secure ways to do this is by using 


SFTP - Secure File transfer Protocol
This used the SSH file transfer protocol so 
TCP port 22 

This provides File system functionality, allowing directory listing and remote file removal and it used ssh for its encryption 



FTP - File transfer Protocol
TCP
This uses two different port numbers to accomplish this file transfer
TCP port 20 is for active mode data
Active mode data is where we are actually transferring the file
TCP port 21 is for Control Mode data 
The control process which usually tells the system which device to send operates over port 21

FTP has authentication functionality and full featured functionality 

There's a less functional version of FTP called


TFTP or Trivial File transfer Protocol
UDP 
Operates on UDP port 69 
this offers very simple file transfer application to read files and write files.
Not used on production systems 




DHCP:
dynamic host configuration protocol.

This is the automated configuration of Ip addresses, subnet masks and other options

UDP 
Operates on UDP ort 67 and UDP port 68 to Provide this functionality

This requires a DHCP server, Often Included in many SOHO routers 

Your DHCP server usually has a group of IP addresses that can be handed out to devices this is called a pool of Ip address, and there is a lease time associated with the pool so you assign the IP address and tell the device it is able to use that IP address for a time period after that time period that device has to renew that IP address or it would have to release the IP address, These are dynamic IPs

Some Network Admins may also reserve IP addresses inside the DHCP server my associated the MAC address to a specific IP address so every time a particular server is started it always receives the same one 



HTTP and HTTPS:
Hypertext transfer Protocol
Communication in browser

If its unencrypted over HTTP you are gonna be using most likely 
port 80 TCP

while if its Encrypted you will use 
Port 443 TCP With TLS/SSL encryption



SNMP - Simple network management protocol:
Network admins often have to configure switches routers and other devices on the network and to be able to check in and gather statistics from those devices we can use SNMP 
UDP
Operates over UDP port 161 

The SNMP Service that you are using comes in different versions

The og is 

V1 - this is where there are very structured tables and all of the data is sent over the clear in the network 


There was a update to v1 called

v2 - this update allows for bulk transfers, but is still in the clear and unencrypted

the most common version you will see on networks is 

v3 - There is encryption, there's message integrity, and authentication 

Not only can we query these devices using UDP port 161 we can tell this device that if anything bad happens to send an alert message to us This is called an SNMP trap and it sends that Trap over UDP port 162 



Syslog: 
one challenge for a network security pro is finding out what these devices are doing on the network, and one of the most common ways to accomplish this is by examining the logs of every device, but instead of manually going to every device to be able to see these logs we instead have all of these devices send their logs into one central repository we are able to do this using a standard protocol called, 

Syslog 
UDP
operates of UDP port 514
Usually all of this log information has a single repository or collection and is integrated into a SIEM (system Information event manager) 
as you can imagine all this log info will need alot of disk space to store





RDP - Remote Desktop Protocol

This shares a GUI desktop view to a remote location

TCP 
operates over TCP port 3389





NTP - Network Time protocol 
Earlier we talk about log file consolidation but its important when looking at a log that we are able to see what time these logs were collected so you need to ensure all devices have the same time configured.

We are able to do this using NTP every device on your network probably has an NTP configuration option and NTP uses
UDP 
port 123



SIP - Session Initiation Protocol 
If you have Ever used a Voice over IP phone or used VOIP software then you have probably used SIP protocol,
we refer to SIP as a signaling protocol its able to setup the phonecall, and teardown the phonecall when over  and set parameters about the phone call while in use
we commonly use 
TCP 
TCP port 5060 and Tcp port 5061 for the session initiation protocol,
we refer to SIP as a signaling protocol cause its in charge of these voice communications, When you place a call when you hang up and when it rings SIP handles all of this. 



SMB - Server message block:
if you have ever transferred a file form one windows computers to the other or sent a job to a printer then you have probably used Server message block 
Commonly referred to as CIFS (common internet file system )

Most windows computers use SMB over TCP port 445 where it is a direction communication from one device to the other previous version of windows use netBIOS but when using tcp port 445 is is netBIOS-less without the need of its support 


Another common service on our production networks is having an centralized database where you can store info about users, like their usernames and passwords and other important info. To be able to access this information we would use 

LDAP OR (lightweight Directory Access protocol) 
TCP
which operates over TCP port 389 
Unencrypted

There's a secure version called

LDAPS:
this is LDAP but encrypted with SSL/TLS encrypted
uses TCP port 636



Databases:
Another common service on network is access to a database and there's are different protocols for different databases 


Microsoft SQL server 
MS-SQL 
Uses TCP port 1433

Oracle SQL *Net*
also called Oracle Net or Net8
Operates over TCP port 1521


MySQL 
This is a free open DB 
Uses TCP port 3306
