
Many network admins like to separate their networks into different Broadcast domains, this is sometimes done to allow additional security features or we may need to provide separation just to keep the network organized. 

One way you could do this is to have completely separate switches, because these are physically separated the two separated networks cant communicate, usually this is a waste of resources alot of times.



Local Area Network (LAN):
- This is a group of devices in the same broadcast domain 





Virtual Local Area Network (VLANs):
- this is a way to separate a LAN into two LANs logically instead of physically   ![[Screenshot 2024-07-16 021605.png]]



In most organizations though there may be multiple switches, we may need to connect devices that are on One VLAN on one switch to the same VLAN on a separate physical switch ![[Screenshot 2024-07-16 021722.png]]

In this example above we wanna connect the Two VLAN 100s together and the two VLAN 200s together.

An easy way to this is just with an ethernet cable like shown in the picture. SO extend an ethernet cable from VLAN 100 on one switch to the VLAN100 interface on the other switch and do the same with VLAN200. This wont scale very well especially say if you had 20 VLANs on these switches,



VLAN trunking:
Instead of extending separate ethernet cables for each individual VLANs, we can extend a single connection and communicate all VLANs across that single connection. We refer to this as VLAN trunking. You may also see this referred to as the 802.1Q Ethernet Trunking standard.![[Screenshot 2024-07-16 022050.png]]




VLAN header:
the process of adding and removing a header is pretty simply all we do is after the Source MAC address and before the Ethernet type Header we just add a VLAN header which contains info about which VLAN is associated with the data ![[Screenshot 2024-07-16 022306.png]]











Data and voice cabling:
We only need one cable for both network connectivity on our Computer and phone. we can do this by plugging our computer into our phone then plug the phone then there would be a seperate ethernet connection from the phone to the switch in the closet close ![[Screenshot 2024-07-16 022618.png]]


VOIP and other data doesn't like each other, One way we resolve this is we put the computer on one VLAN and the phone on another ALOT of switch interfaces have both a data VLAN and voice VLAN 