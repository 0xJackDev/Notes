
The role of a switch is to forward traffic based on the destination MAC address inside of an ethernet frame. Meaning the switch needs to keep an ongoing and active list of all of the devices it happens to know about based on the MAC address of the devices. The switch builds this by examine inbound traffic and looking at the Source MAC address and tying that Source MAC address to a specific physical interface. And with switches configured with Spanning Tree Protocol (STP) they're also responsible for making sure a loop doesn't occur on the network.


The process of sending traffic through a switch network is the same for every ethernet frame. 

When sent An ethernet frame the Switch looks at the packet and if the Destination MAC address is in the List of MAC address, it sends the Data to the output interface matching that MAC address. If you have multiple switches its the same process but occurring twice. 



Building the MAC address table is extremely important, with no MAC address table the switch doesn't know where to send the traffic. To build this the Switch looks at all incoming traffic and Notes the Source MAC address, It adds Unknown MAC addresses to the MAC address table. It will then associate that Source MAC address to a output interface on the switch.



If a switch does not have an Entry for that MAC address then it will send that information to everyone on the network. And then whoever the data was meant for will reply back to the switch and then it will log the Source MAC address 





On a IPv4 Network devices are able to obtain the MAC address of a remote device using

Address Resolution Protocol (ARP):
This determines a MAC address based on a IP address 
- this works by querying the network with a IP address and that IP address will respond back with its MAC address
- your local computer keeps a cache of all the MAC addresses it knows you can see the ARP table with arp -a 







Neighbor Discovery Protocol (NDP):
this is literally just ARP in IPv6 but since there's no Broadcast in Ipv6 we use multicast 
- Replaces Ipv4 ARP 
- Can be used in conjunction with SLAAC (stateless address autoconfiguration) to auto configure a IP without a DHCP server 
- Uses multicast 
- NDP also uses Duplicate Address Detection (DAD) to make sure there's no duplicate IPs







Power Over Ethernet (PoE)
- This is power provided over an ethernet cable 
- One wire for both Network and Electricity 
- Useful for difficult to power area
- Power usually comes from the switch if this is true its called an Endspans if its a In-line power inject its a Midspan 
- -IEE 802.3af-2003 this is the Original PoE standard
- POE+: IEEE 802.3at-2009