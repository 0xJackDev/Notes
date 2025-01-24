wHEN DEPLOYING iPV6 tHERE ARE A NUMBER OF WAYS you can implement this in your environment, One wall is to tunnel the Ipv6 Within an existing network Configuration for example. 


6to4 addressing:
this is a type that sends Ipv6 Information  over an existing Ipv4 Address, Basically creating a Ipv6 address based on the Ipv4 address, 
This requires Specific relay routers that are designed for this Tunnelling
There is no support for Network Address Translation (NAT) which certainly limits the ability to send this traffic across the internet 

The reverse to 6to4 is 

4in6 Tunneling 
where you would tunnel Ipv4 traffic on a existing Ipv6 network 


If you wanna Tunnel Ipv6 but wanna support NAT then use 


Teredo 

This Tunnels IPv6 through a NATed IPv4 network, 
allowing you to send it end to end IPv6 through an Ipv4 network
No special Ipv6 router needed 
- this is designed to be temporary 

While Teredo is seen on windows machines theres a linux Alterative called

Miredo 
- same  thing foor linux



Todays Implementations of Ipv6 tend to be End to end and we Implement this using

Dual-stack Routing:
This means that our devices and our routers Can communicate using both Ipv4 and Ipv6 At the same time, You can send Data to either Address and it will forward it properly 

With Ipv4, you would configure a router or a device with an Ipv4 address, Using a Ipv4 routing table and Ipv4 dynamic routing protocols, The same Config As normal What we have done is add an additional protocol on our routers for 

Ipv6:
Theres a separate Configuration for Ipv6 Addresses, These devices have their own Ipv6 routing tables, and This maintains a separate Ipv6 Dynamic Routing protocols and Tables. 




If you are using Ipv6 you will notice Ipv6 doesn't use broadcast, There's no ARP in Ipv6 
We removed broadcast completely from the Protocol, but we still need other ways to identify devices on a network, but without broadcast we cant Use ARP to find Devices so instead we use a specialized Multicast protocol called:



Neighbor Solicitation (NS):
This is sent as Multicast, so it sends to Multicast TO a Ipv6 address and whoever matches the request will Send the Response Back as a Neighbor Advertisement or (NA)![[Screenshot 2024-07-12 231909.png]]



This allows us to Use more efficient protocols like multicast and replace the functionality of ARP with the 
NDP (Neighbor Discovery Protocol ):
Lets use Use Multicast With ICMPv6

This Allows Neighbor MAC discovery

IPv6 also provides us with a way to statically address devices called without a DHCP server

SLAAC (Stateless Address Autoconfiguration):
this auto configures an IP address without dhcp 


to be able to support SLAAC we need to use

DAD (duplicate Address Detection):
to make sure theres No duplicate IPs used in SLAAC 


This is also what we use to discover routers on our Network, NDP would send a Router Solicitation (RS) packet, and listen for a Router Advertisement packet (RA), Allowing Local devices to automatically configure themselves and identify where the routers are on their local subnet,
![[Screenshot 2024-07-12 232358.png]]