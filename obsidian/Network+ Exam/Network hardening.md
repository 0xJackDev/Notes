

Secure SNMP:
- Using SNMPv3 makes sure your traffic is encrypted so don't use any versions before this 
- Use SNMPv3 everywhere you can






Router Advertisement (RA) guard:
- This protect IPv6 Router Advertisement Which is like ARP for Ipv6
- a rogue device could pretend to be a router,  so switches can turn on Router advertisment guard to Validate the RA messages 





Port security:
- Prevent unauthorized users from connecting to a switch interface
- Based on the source MAC address and if that MAC address doesnt match a configuration you have previously configured on that switch, then you can make a decision on what to do with the traffic for example drop it




Dynamic ARP inspection (DAI):
- Arp is powerful but has no security, Someone can pretend to be a different device on the network by spoofing their IP address and then now in the ARP table its gonna be linked to the attackers MAC address and send all data to them
- DAI prevents this, If you turn on DAI in the switch you can prevent those nasty on path attacks and stop ARP poisoning at the switch level 
- DAI relies on creating a map of all devices on your network using DHCP snooping for intel 
- This intercepts all ARP requests and responses and only valid requests make it through






Control Plane Policing:
Modern networking devices have different planes of operations the plane that handles forwarding of data is called the Data plane or Control Plane.
- Control plane manages the device 
- Very important to secure, Defines a QoS filter to protect the control plane
- Control packets should have priority
- Manage traffic, Prioritize management traffic and block unnecessary control plane traffic types, 



Private VLANs:
- Port Isolation 
	- restricts access between interfaces even when they are in the same VLAN 
	- I.E Ports cant talk to each other 




Disable Unused interfaces 
- Can dp this with NAC, 802.1X




Disable Unnecessary ports and services
- Every Open Tcp/UDP port on a device is a possible entry point
- Close everything except required ports
- You can commonly control this access with a firewall, NGFW is ideal
- Any unknown services should be disabled or filtered from network communication
- Use NMAP to scan for what ports are open. 




- Change default credentials



Very easy to find defaults for your access point / router 
https://routerpasswords.com


Make your password complex




DHCP snooping:
- theres no security built into DHCP 
- We can add additional security within our switches by enabling DHCP switches
- allows us to track IP addresses and MAC addresses on our Layer 2 Switch
- The switch essentially becomes a DHCP firewall
- You configure the switch to trust firewalls, routers and DHCP servers 
- And anyone who isnt trusted like other computers or unofficial DHCP servers 
- Switch watches for DHCP conversion and adds a list of untrusted devices to a table
- Filters invalid IP and DHCP information, for example If you tried to spoof your IP address to poison an ARP cache it would see that the device with that source IP has a different MAC address then its record for that IPs MAC address and know sum fishy 






Change default VLAN:
- all access ports (non-trunk ports) are assigned to a VLAN 



Upgrading firmware:
- many network devices don't use a traditional operating system
- All updates are made to firmware 
- its harder to update firmware as its embedded into the device 




Role-based access:
- not everyone needs access to connect to a switch for example, so not everyone needs the same level of access








Access control Lists (ACLs):
Allows or disallows traffic based on tuples
- tuples could be source IP, destination, Ip, Port number, time of day, etc 
- You could restrict access to network devices by limiting by IP address
- 