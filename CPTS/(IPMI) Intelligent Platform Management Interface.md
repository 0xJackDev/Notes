
Port 623 commonly

It is important to understand that IPMI is usually and should only be accessible from the internal network.

## About IPMI
IPMI is a set of standardized specification for hardware-based host management systems used for system management and monitoring. It acts as a autonomous subsystem and works independent of the hosts BIOS, CPU and firmware. IPMI allows sysadmins with ability to manage and monitor systems even if they are powered off or in a unresponsive state. It operates using a direct network connection to the systems hardware and does not require access to the operating system via a login shell. IPMI can also be used for remote upgrades to systems without requiring physical access to the target host. IPMI is used in three ways:

- Before the OS has booted to modify BIOS settings
- When the host is fully powered down
- Access to a host after system failure.


When not being used for those tasks, IPMI can monitor a range of different things like voltage system temp and basically anything you can think of you can measure on system hardware. including alerting using SNMP.



IPMI protocol was published by Intel in 1998 and is now supported by over 200 sys vendors. 




## Footprinting 


Like stated IPMI communicates over port 623 UDP. so use -sU to look for UDP ports. Systems that use IPMI protocol are called baseboard management controllers or (BMCs). BMCs are typically implemented as embedded ARM systems running Linux and connected directly to the motherboard of the host/ BMCs are built into many motherboards but can also be added to a system as a PCI card. Most server either come with a BMC or support adding a BMC. The most common BMCs we see during internal pen tests are HP, iLO, Dell DRAC, and Supermicro IPMI. If we can access a BMC during an assessment we would gain full access to the host motherboard and be able to monitor, reboot, power off or even reinstall the host operating system. Many of these BMCs include a web-based management console, some sort of command-line access like ssh or telnet, and the port 623 for the IPMI network protocol over.

Below is a sample Nmap scan using the Nmap [ipmi-version](https://nmap.org/nsedoc/scripts/ipmi-version.html) NSE script to footprint the service.

#### Nmap

IPMI

```shell-session
JackTheWizard@htb[/htb]$ sudo nmap -sU --script ipmi-version -p 623 ilo.inlanfreight.local

Starting Nmap 7.92 ( https://nmap.org ) at 2021-11-04 21:48 GMT
Nmap scan report for ilo.inlanfreight.local (172.16.2.2)
Host is up (0.00064s latency).

PORT    STATE SERVICE
623/udp open  asf-rmcp
| ipmi-version:
|   Version:
|     IPMI-2.0
|   UserAuth:
|   PassAuth: auth_user, non_null_user
|_  Level: 2.0
MAC Address: 14:03:DC:674:18:6A (Hewlett Packard Enterprise)

Nmap done: 1 IP address (1 host up) scanned in 0.46 seconds
```


Here, we can see that the IPMI protocol is indeed listening on port 623, and Nmap has fingerprinted version 2.0 of the protocol. We can also use the Metasploit scanner module [IPMI Information Discovery (auxiliary/scanner/ipmi/ipmi_version)](https://www.rapid7.com/db/modules/auxiliary/scanner/ipmi/ipmi_version/).


#### Metasploit Version Scan

IPMI

```shell-session
#Scan version info
msf6 > use auxiliary/scanner/ipmi/ipmi_version 

#Dump Hashes
msf6 > use auxiliary/scanner/ipmi/ipmi_dumphashes 
```


During internal penetration tests, we often find BMCs where the administrators have not changed the default password. Some unique default passwords to keep in our cheatsheets include:

|Product|Username|Password|
|---|---|---|
|Dell iDRAC|root|calvin|
|HP iLO|Administrator|randomized 8-character string consisting of numbers and uppercase letters|
|Supermicro IPMI|ADMIN|ADMIN|

It is also essential to try out known default passwords for ANY services that we discover, as these are often left unchanged and can lead to quick wins. When dealing with BMCs, these default passwords may gain us access to the web console or even command line access via SSH or Telnet.


## Dangerous Settings

If default credentials do not work to access a BMC, we can turn to a [flaw](http://fish2.com/ipmi/remote-pw-cracking.html) in the RAKP protocol in IPMI 2.0. During the authentication process, the server sends a salted SHA1 or MD5 hash of the user's password to the client before authentication takes place. This can be leveraged to obtain the password hash for ANY valid user account on the BMC. These password hashes can then be cracked offline using a dictionary attack using `Hashcat` mode `7300`. In the event of an HP iLO using a factory default password, we can use this Hashcat mask attack command `hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u` which tries all combinations of upper case letters and numbers for an eight-character password.

There is no direct "fix" to this issue because the flaw is a critical component of the IPMI specification. Clients can opt for very long, difficult to crack passwords or implement network segmentation rules to restrict the direct access to the BMCs. It is important to not overlook IPMI during internal penetration tests (we see it during most assessments) because not only can we often gain access to the BMC web console, which is a high-risk finding, but we have seen environments where a unique (but crackable) password is set that is later re-used across other systems. On one such penetration test, we obtained an IPMI hash, cracked it offline using Hashcat, and were able to SSH into many critical servers in the environment as the root user and gain access to web management consoles for various network monitoring tools.

To retrieve IPMI hashes, we can use the Metasploit [IPMI 2.0 RAKP Remote SHA1 Password Hash Retrieval](https://www.rapid7.com/db/modules/auxiliary/scanner/ipmi/ipmi_dumphashes/) module.

#### Metasploit Dumping Hashes

IPMI

```shell-session
msf6 > use auxiliary/scanner/ipmi/ipmi_dumphashes 
```




There is gonna be two hashes when you use one The first hash is the IPMI password hash and the second is the session hash

Hash

29ef32ff82000000c5db365f4c332cb27aafc98305f6e2f38771c902fb4e53ddd4f7d37fdd329142a123456789abcdefa123456789abcdef140561646d696e

-m 7400 

## Hashcat

When using the msf module to retrieve hashes they can be cracked using a dictionary attack and hashcat mode 7300. 

In the event of a HP iLO using a factory default password instead of using a wordlist we can use this Mask attack command to try all combinations of upper case letters and numbers for an 8 character password

`hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u` 


I was having issues with hashcat but looking the options you can actually see the pass_file and output_hashcat_file so I set the first to rockyou.txt and the second to output.

Since i made it use the rockyou password I get the password with this. using the ipmi_dumphashes module