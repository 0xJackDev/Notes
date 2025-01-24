
We will  go over the setting configurations of Switches interface 


Basic Interface configuration:

- Speed and Duplex, This refers to the speed of the ethernet link. And duplex refers to the state of data either being able to be sent and received at same time or not. Many times this configuration is automatic but can be configured manually
- IP address management, This is gonna be there if you have any VLAN interfaces, or if its a Layer 3 switch with routing capabilities you gotta configure the IP address, subnet mask, DNS and more there as well as the routing table. 






VLANs:
If you are configuring a switch you may have to configure what VLAN is associated with what that physical interface, every port on a switch should be assigned on a VLAN.
- You may also need to configure VLANs across trunk configurations or define what VLANs are able to traverse a particular trunk which would allow you to connect multiple switches together and maintain communication between different VLANs
- Some communication will not include a VLAN header data without this is called untagged Frames these frames will be on the default VLAN also called the native VLAN. The rest of the VLANs will traverse the trunk by having a tag added to the ethernet header  and that tag will be removed on the other side of the trunk. 





LAG and mirroring:

Lag:
- Having a singe link to connect switches is useful for connectivity but you may need more bandwidth for switches. There's a standard that allows you to put multiple connections between switches and use all of those connections as one aggregated link. This what's called Port bonding or Link aggregation (LAG). These ports will act as one big port and often be controlled by a protocol this protocol is LACP or (Link aggregation Control Protocol) 


Port mirroring 
- If troubleshooting a switch, you may find it difficult to be able to see the packets that are traversing to individual devices, if you need to capture some of this info you may want to configure one of these interfaces as a port mirror.
- a port mirror will copy traffic from one or more interfaces on a switch to a separate interface that you can then plug and and perform packet captures with to monitor traffic 
- when we use a switch to perform this port mirror we will hear this called a SPAN (switch port analyzer connection) or a network tap 




Jumbo frames
A standard ethernet frame supports 1500 bytes of payload. If performing a very large file transfer it may be more efficient to have larger payload size this is supported in ethernet by a function called Jumbo frames. 

- You can increase the payload size to 9,216 bytes but 9000 is the norm.
- this increases Transfer efficiency because you dont have to send as many packets 
- Ethernet Devices must support jumbo frames so you have to configure all devices you are using to support Jumbo frames 






Ethernet flow control:
One problem with ethernet is that it is non-deterministic meaning there's no way to determine how fast or slow traffic will be sent over this network. If  a file transfer overwhelms the network we need to have some way to tell the other device to slow down the amount of data. 
- One popular way to manage this traffic is to use IEEE 802.3x 
- called The "pause" frame 
- sends a message to the other device telling it to pause for a second






Port Security:
One concern we have with installing ethernet connection is someone could walk in from inside, plug in their devices and gain access to our internal network. 
- One way to prevent this is to Configure a interface on the switch to have Port security, this would prevent unauthorized users for connection to a switch interface
- This Could alert or Disable the port
- This Is based on the source MAC address so it can be bypassed by port spoofing......
- Each port should have its own config and unique rules for only unique MAC addresses in our own organization
- Configure a number of whitelisted MAC addresses for switches. The switch will monitor the number of unique MAC addresses, if the number of MAC addresses exceeds the amount of MAX mac addresses it would begin to disable interfaces. Really port security can be changed and configured by the network admin