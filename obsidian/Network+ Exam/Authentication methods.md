

Local Authentication:
if you have a wireless router at home you probably had to connect to the device to make configuration changes in which it asked for a username and password, that username and password is often stored on the device itself. 
- We refer to this as Local Authentication
- Where authentication credentials are stored on the local device 
- Very manual process, must be individually administrered
- Doesn't rely on a third party authentication server






Multi-Factor authentication:
More than one factor
- Something you are 
- Something you have 
- Something you know 
- Somewhere you are
- Something you do


- This could be expensive like for example a hardware token
- Could also be very inexpensive









RADIUS (Remote authentication dial-in user service):
There are many different types of authentication services you can have running on your authentication server one common is RADIUS.
- One of the more common AAA protocol 
- This provides a centralized databased on usernames and passwords for routers, switches, firewalls or maybe a server or maybe remote VPN access
- One of the most popular types of authentication 





TACACS (Terminal Access Controller Access-Control System):
another common type of remote authentication protocol is TACACS.


Its more common these days to use

TACACS+ being used 
- More standard version of TACACS 
- Authentication protocol








LDAP (Lightweight Directory Access protocol):
- Another common authentication protocol
- This is a protocol for reading and writing directories over an  IP Network
- Uses a standard for the International Telecommunications Union (ITU) called X.500 
- this X.500 Was originally used with DAP but LDAP replaced it so it was more lightweight on our systems
- LDAP is the protocol used to query and update an X.500 directory 
- Used in windows Active directory 






Kerberos: 
- Network authentication protocol 
- You can authenticate once and you are trusted by the system with no need to re-authentication
- SSO (single sign on) protocol 
- Supports Mutual Authentication where the server and client authenticate to each other like WPA3 preventing On-path and replay attacks
- Standard made in 1980
- Integrated into windows and other operating systems


SSO with Kerberos: 
- Kerberos is able to assign this SSO capability with a lot of backend Cryptographic ticketing 
- You login with your username and password and its remembered by the system whenever you try to connect to other resources on the network Allowing you to login with one set of credentials and reach other things on the network
- Not everything is Kerberos Friendly as Kerberos has a advanced Back-end and not all devices support it
- There are other SSO methods 









Which method to use?
This is often determined  by what you are trying to install for example a VPN concentrator can talk to a RADIUS server, Or if you already have a RADIUS server it'd probably be easiest to just use that

- TACACS+ 
	- This is usually a CISCO router or switch if your using TACACS+ to authentication



Kerberos and LDAP
- probably a Microsoft network






IEE 802.1X:
- Port-based network Access control (NAC) 
- You don't get access to the network until you authenticate it will block the port until you do 
- EAP integrates with 802.1 (extensible authentication protocol)
- Often used in conjunction with a Authentication database 










Extensible authentication protocol (EAP):
- An authentication framework
- Many different ways to implement
- Integrates with 802.1X for Authentication