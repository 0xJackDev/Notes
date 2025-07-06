UDP port 161

Simple Network Management (SNMP) is created to monitor network devices. This protocol can also be used to handle configuration tasks and change setting remotely. SNMP-enabled hardware includes switches, routers, servers and IoT devices and many other network devices that can be queried. These are all controlled use the SNMP standard protocol so it is a managment and monitoring protocol. 



SNMP also trasmits control commands using agents over UDP port 161. The client can set specific values in the device and change options and setting with these commands. While in classical communication it is always the client who request info from the server. SNMP enables the use of so-called traps over port 162. These are data packets sent from the SNMP server to the client without being requested think of it like a cronjob that runs every time a specific event occurs on the server-side. 

for the snmp client and server to exchange values. the available SNMP objects (aka routers servers etc) must have unique addresses known on both sides. This addressing mechanism is absolute prequel for successfully transmitted data and network monitoring using SNMP


## MIB

To ensure that SNMP access works across different products with different manufactures. The Management information base (MIB) was created.  MIB is an independent format for storing device information. A MIB is a text file in which all query able SNMP objects of a device are listed in a tree hierarchy. It contains at least one Object Identifier (OID) which in addition to the unique address and a name, also provides info about the type of device, access rights, and a description of the object MIB files are written in the Abstract syntax notation one.


## OID
An OID represents a node or a device in a hierarchical namespace. A sequence of numbers uniquely identify each node, allowing the nodes position in the tree to be determined. The longer the chain the more specific the info. Many nodes in the OID tree contain nothing except references to those below them. The OIDs consist of integers are usually contratied by dot notation. We can look up many MIBs for the associated OIDs in the [Object Identifier Registry](https://www.alvestrand.no/objectid/).


## SNMPv1

SNMP v1 is used for network management and monitoring. SNMPv1 is the first version of the protocol and is still in use in smaller network. The problem with SNMPv1 is there is no built in authentication. It also does not support encryption.


## SNMPv2
SNMPv2 existing in different versions. The version that still exists today is v2c, and the c extension means community based. SNMPv2 is on par with SNMPv1 but has been extended with additional functions from the part-based SNMP no longer in use. However the problem with the inital execution of the SNMP protocol is that the community string that provides security is only transmitted in plain test. Also can be bruteforced usually



## SNMPv3 
the security has been increased enormously for SNMPv3 by security features like authenticate using username and password. and using encryption via a preshared key.


## Community strings
Community strings can be seen like passwords that can be used to determine whether the requested information can be viewed or not. It is important to note many organizations use SNMPv2 still as the change to SNMPv3 can be very complex.  

We can look up many MIBs for the associated OIDs in the [Object Identifier Registry](https://www.alvestrand.no/objectid/).

#### SNMP Daemon Config

SNMP

```shell-session
JackTheWizard@htb[/htb]$ cat /etc/snmp/snmpd.conf | grep -v "#" | sed -r '/^\s*$/d'

sysLocation    Sitting on the Dock of the Bay
sysContact     Me <me@example.org>
sysServices    72
master  agentx
agentaddress  127.0.0.1,[::1]
view   systemonly  included   .1.3.6.1.2.1.1
view   systemonly  included   .1.3.6.1.2.1.25.1
rocommunity  public default -V systemonly
rocommunity6 public default -V systemonly
rouser authPrivUser authpriv -V systemonly
```

The configuration of this service can also be changed in many ways. Therefore, we recommend setting up a VM to install and configure the SNMP server ourselves. All the settings that can be made for the SNMP daemon are defined and described in the [manpage](http://www.net-snmp.org/docs/man/snmpd.conf.html).



## Dangerous settings

Some dangerous settings that the administrator can make with SNMP are:

|**Settings**|**Description**|
|---|---|
|`rwuser noauth`|Provides access to the full OID tree without authentication.|
|`rwcommunity <community string> <IPv4 address>`|Provides access to the full OID tree regardless of where the requests were sent from.|
|`rwcommunity6 <community string> <IPv6 address>`|Same access as with `rwcommunity` with the difference of using IPv6.|



## footprinting

for footprinting we use tools like snmpwalk, onesixtyone and braa. Snmpwalk is used to query the OIDs with their information. onesixtyone can be used to brute-force the names of community strings since they can be named by admins. Since these community strings can be bounds to any source identifying the existing strings can take some time.



#### OneSixtyOne

SNMP

```shell-session
JackTheWizard@htb[/htb]$ sudo apt install onesixtyone
JackTheWizard@htb[/htb]$ onesixtyone -c /opt/useful/seclists/Discovery/SNMP/snmp.txt 10.129.14.128

Scanning 1 hosts, 3220 communities
10.129.14.128 [public] Linux htb 5.11.0-37-generic #41~20.04.2-Ubuntu SMP Fri Sep 24 09:06:38 UTC 2021 x
```


Once we know a community string, we can use it with [braa](https://github.com/mteg/braa) to brute-force the individual OIDs and enumerate the information behind them.

#### Braa

SNMP

```shell-session
JackTheWizard@htb[/htb]$ sudo apt install braa
JackTheWizard@htb[/htb]$ braa <community string>@<IP>:.1.3.6.*   # Syntax
JackTheWizard@htb[/htb]$ braa public@10.129.14.128:.1.3.6.*

10.129.14.128:20ms:.1.3.6.1.2.1.1.1.0:Linux htb 5.11.0-34-generic #36~20.04.1-Ubuntu SMP Fri Aug 27 08:06:32 UTC 2021 x86_64
10.129.14.128:20ms:.1.3.6.1.2.1.1.2.0:.1.3.6.1.4.1.8072.3.2.10
10.129.14.128:20ms:.1.3.6.1.2.1.1.3.0:548
10.129.14.128:20ms:.1.3.6.1.2.1.1.4.0:mrb3n@inlanefreight.htb
10.129.14.128:20ms:.1.3.6.1.2.1.1.5.0:htb
10.129.14.128:20ms:.1.3.6.1.2.1.1.6.0:US
10.129.14.128:20ms:.1.3.6.1.2.1.1.7.0:78
...SNIP...
```


https://docs.opsramp.com/solutions/monitors/snmp-monitors/how-to-execute-snmpwalk/




Since SNMP is a udp protocol we must use a UDP port scan to see it

sudo nmap -sC -sV 10.129.58.255 -p 161,162 -sU


so from this i find out its SNMPv1 and i use SNMPwalk

snmpwalk -v 1 -c public 10.129.58.255


and find the EMAIL address and more info


PORT    STATE  SERVICE  VERSION
161/udp open   snmp     net-snmp; net-snmp SNMPv3 server
| snmp-info:
|   enterprise: net-snmp
|   engineIDFormat: unknown
|   engineIDData: 5b99e75a10288b6100000000
|   snmpEngineBoots: 11
|_  snmpEngineTime: 10m33s
162/udp closed snmptrap