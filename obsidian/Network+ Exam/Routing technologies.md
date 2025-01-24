When you send traffic across the internet. That traffic is stopping at every router along the way and asking for directions. The directions that a packet should go are contained within a routing table. 

Routing table:
Every packet has a list of directions and when a packet is inbound the router looks at the destination IP address and determines what the best Route would be Depending on the Dynamic Routing Protocol used. This is based on a list of predetermined routes. That packet then makes its way to the next router and that router performs the same lookups to its routing table and determines where its next route might be.

Any device that needs a decision on where Traffic goes Is gonna need and have a routing table. Routing tables in routers, workstations and other devices.


The Hop:
When these packets traverse a router we refer to this as a hop. Whenever we talk about what the next Hop might be we are referring what the next router might be we are gonna know to "hop to". If you look at the routing table in a single Router, it doesn't have to know the entire path from point A to point B. It only has to know what the next hop will be to get that packet on its way.
You will find that there are routes listed in the Routing table that are specific for the Locally connected interfaces. But very often there would be a default route that would be once you go through every possible option and none of those match the destination, use this particular link as the default. 

As you can imagine with many packets and many routers sometimes you can create a loop, Where router A says to Send the Packets to Router B but B says to send them to A. In order to identify and resolve this Ipv4 has a Mechanic called Time to live or TTL, that counts every hop and decreases the TTL by 1 every time and once the TTL is 0 it drops the packet. Ipv6 has a similar function but calls it a Hop limit





Configuring the next hop:
When configuring a router, you may be setting it up for a dynamic routing protocol, so the router determines the best route to be. OR you might be configuring this manually with Static routes in which you tell the router where the destination and next hop should be. Every router has to be configured with a routing table. So that any inbound communication knows where to go as its next hop. 
A router that's not configured properly or has an incorrect next hop will end up in a routing problem, its easy that this will create a routing loop.




Default Routes:
This is the route you take when no other routes match, 
- the gateway of last resort

If you are looking at a computer on a remote site, the Remote site might only have one possible route in that situation the Default route would always be used commonly this default route is defined by 0.0.0.0/0 

- This dramatically simplifies the routing process 







Routing Metrics:
Each routing protocol has its own way of calculating the best route

Metric values are assigned by the routing protocol but for example RIPv2 Metrics are useful or OSPF or EIGRP.

Use metrics to choose between redundant links.




Routing tables:
![[Screenshot 2024-07-16 000805.png]]

Our Gateway address is gonna be our next hop. So we send our Packets from interface 192.168.1.22 to 192.168.1.1 is our next hop. And destination 0.0.0.0 Just means that our destination isnt in the Routing table. 
So thats the first hop, nows its at the router

The router is performing NAT so ![[Screenshot 2024-07-16 001137.png]]
If we are sending Traffic out Of our local subnet then the IP we are gonna use for the Interface for sending outs gonna be 10.1.10.14 but if we are sending stuff in our LAN it will be 192.168.1.1. And if we send it to a IP address that's not in that table it will use the default gateway of 10.1.10.1 and send it to router 10.1.10.1 .

The last router will then get the packet and most likely perform NAT and turn it back into another networks  IP address  (the reason its changing IP again is because its going on the ISPs control) and send it on through its network. 


Incase any traffic flows from the internet to the Router of 74.208.221.234 then there has to be an entry in the routing table that tells the traffic if any traffic is going down to 192.168.1. network it needs to go to the next hop of 10.1.10.14 




Routing table issues:
When troubleshooting routing problems, you must go to every device with a routing table and examine what that routing table might be. To make sure the flow of traffic is going the way you want. Say that we didnt know Our ISPs gateway to send the info out of our network to into theirs. Well then if we just put a random number it wouldn't work we needa know the IP address of the gateway next hop. 





Administrative Distances:
You may find that there are routers on your network that use many dynamic routing protocols to be able to build its routing table. This is not uncommon for a internet facing router when you have OSPF inside your internal network and BGP on the internet side of your network. 
Since using Two different routing protocols we will have completely different metrics and cant compare them but we still need to determine which route to use when we have this conflict.

this is where Administrative Distances come in to determine what routing protocol has priority over the other.![[Screenshot 2024-07-16 002008.png]]


Here is the chart to determine which Protocol is best.



Managing Network Utilization.
its not enough to just know where the next hop might be. We also have to set priortes over the type of traffic going across our network.
For example a real-time system like VOIP would need priority over something that can be delayed. 
Some applications are more important then others and you need to determine this. 




Traffic shaping:
the method for prioritizing traffic on your network is usually called Traffic shaping or packet shaping. 