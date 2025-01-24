
ICMP - Internet Control Message Protocol 
In this we have talked about two Normal Protocols you see running inside of IP which is TCP or UDP, but there is other protocols which we might fit inside of IP one of which is

ICMP,
you can think of this as a way of devices to send messages to each other 
This is not used for transferring data but more commonly used for management and control of devices across network 
For example you might use the ping command to see if another device on the network will reply. when sending a Ping you are sending a ICMP packet and receiving a ICMP packet back in response, when things go wrong its usually verbose and tells you 




GRE - Generic Routing Encapsulation:
one common way to communication, either between sites or devices is to create a tunnel between those devices and send our data through that tunnel, One way to create this tunnel is to use GRE Protocol 

GRE allows us to encapsulate other types of data within a IP packet and send that info to a remote site, when you use GRE it appears that the two devices communicating appear to be directly connected, there is no Built in encryption to GRE so we need to add additional protocols inside GRE for that security 


VPNs: virtual private networks 
One common way to Encrypt data over these tunnels is to use VPNs or virtual private networks,
This allows you to send encrypted data 
To do this we commonly need a VPN concentrator, this is the device that is going to encrypt and decrypt the data we are going to be sending over this tunnel, this is commonly integrated into firewalls

There is also standalone and software based devices that can perform this functionality
sometimes this is purely software based.


IPsec (internet Protocol Security)
This provides encryption and security for an IP network in OSI layer 3.
Authentication and encryption for every packet
IPsec includes confidentiality/Integrity and anti-replay so you can ensure that no one is resending info thru this tunnel

This is a common way to communicate over a VPN 

There is commonly two core IPsec protocols

One of them is an Authentication header or AH and the other is 
Encapsulation Security Payload or ESP ![[Screenshot 2024-07-13 014047.png]]

As you can see theres two ways to do IPsec Transport mode or Tunnel mode  Tunnel Mode Doesnt encrypt your Typical IP header but 

Tunnel mode Encrypts your OG Ip header and gives you a new one and you add a separate Brand new IP header so anyone looking a this data would have no clue where the True Source Ip was or Were it was going to.


To ensure everything is being sent without any changes we need to add an authentication header, this auth header includes of hash of everything in the packet along with a shared key used by both sides of the communication. 


Of course we wanna make sure the data is encrypted and we able to do thhis using 

Encapsulation Security Payload (ESP)  Protocl
This encrypts the protocol with any choice of encryption algorithm ![[Screenshot 2024-07-13 014445.png]]