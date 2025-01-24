

Heres a common network topology for a SOHO router (small office home office) 
![[Screenshot 2024-07-16 010624.png]]![[Screenshot 2024-07-16 012139.png]]



To understand how traffic gets from one side to another's its useful to examine whats inside the Ethernet frame 


The ethernet frame:
![[Screenshot 2024-07-16 012437.png]]

The IP traffic is inside the Payload



The MAC address:

The mac address is the  Ethernet Media Access control address. 

Ideally every device should have a unique MAC address

- 48 bits / 6 bytes long
- an example is 8c:2d:aa:4b:98:a7

- First three bytes is the OUI or Organizationally unique Identifier 
- the Last three bytes are the Network Interface Controller-specific value. Think of this as the serial number






Duplex:
Duplex describes how we are able to send data between devices. Either One at a time or At the same time


Half-duplex:
- this device cannot send and receive data at the same time, It can either send or receive
- ALL LAN hubs are half-duplex
- Switch interfaces can be configured as Half-duplex or full duplex
- If two devices communicate simultaneously, you have a collision




Full-Duplex:
- Data can be sent and received at the same time 
- A properly configured switch will most of the times be full-duplex




CSMA / CD :
This basic function of Half-duplex is Described as CSMA/CD.
- The CS stands for Carrier Sense, whenever you connect to a network the ethernet device makes sure it is connected to a network with other devices and senses a carrier that its able to use
- the MA stands for Multiple Access. Meaning you can have multiple devices on a network
- the CD stands for Collision Detect. This detects when two stations are talking at once and identify when data gets grabbed
- THIS ISNT USED ANYMORE



