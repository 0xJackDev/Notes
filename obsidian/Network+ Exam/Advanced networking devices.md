
As years have gone by Manufactures realizing putting more capabilities into a single device then they are able to sell more devices a good example of this device is a Layer 3 switch. 




Layer 3 Capable Switch:

This is just a single device with a Switch and a Router in the same physical device. The switching still operates at OSI layer 2 And the routing Still operates at OSI layer 3. The switching and routing both need to be configured separately 






If you have a large wireless network with many Access points then in order for ease of management so you dont have to individually configure each one you will use a 

Wireless LAN controller:
This is a centralized management of access points behind a single "pane of glass".
Using our Wireless LAN controller we can then deploy new access points by sending out the Configuration to that Access point. 
We can perform Monitoring of Security and Performance of access points 
We can make and configure and deploy changes to all sites 
These are usually propertiary meaning if you are using one manufactures Access point you are probably  using their Wireless LAN controller





Load balancer:
This allows Multiple servers to be ran for redudancy For example ![[Screenshot 2024-07-15 160322.png]]


The load balancer can also Provide the Encryption/decryption capabilities and the TCP offload and SSL offload
- we may also cache stuff on the load balancer













IDS / IPS
Intrusion Detection System / Intrusion Prevention System;
these watch network traffic for Exploits, Buffer overflows, Cross site scripting vulns and more.
Intrusion Prevention is more common 








Proxies:
These sit between the users and the external network






Application Proxies:
most proxies in use are application proxies, For example a HTTP proxy is a application proxy that understand HTTP requests and data and Reponses, You could also have a FTP proxy.



VPN concentrator

A vpn creates an ecnrypted tunnel between your device and what your connecting to.

The device you are connecting to is usually a VPN concentrator or Referred to as the Head-end. This provides Encryption and decryption. Is a access device and often integrated into a firewall 

VPN concentrator can also be software running on a client or sometimes built into a OS 



Phone switch::
![[Screenshot 2024-07-15 163644.png]]