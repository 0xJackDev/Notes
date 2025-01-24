

Router:
This allows us to take data on one IP subnet and route that data to a different IP subnet. These may be subnets that are next to each other in the same datacenter or these ip subnets may be located in different parts of the world. We refer to a router as an[[ OSI layer 3]] device. You may sometimes also see this routing function inside an existing switch. These switches are called Layer 3 switches. Its Not that the switch itself is operating on a differ layer, it simple means there is a router and a switch combined into one piece. These routers often connect many different types of networks, LAN's connecting to WAN's, 



Switch:
Switches operate at the MAC address layer or OSI Layer 2 or data link layer device. These switches operate mostly in hardware, The hardware inside of these devices is refered to as an asic. Or a Application Specific Integrated circuit. There are many different functions and capabilities inside these switches. Like for example many of these allow you to include power on the same wires are your ethernet connection and we call this Power over ethernet or (PoE). If the switch includes some type of routing capability into the device with IP then it is a Layer 3 switch


Firewalls:
A traditional firewall allows you to filter traffic based on a TCP/UDP port number. But if you have a more modern firewall then you are probably using a NGFW or a Next generation firewall. Which is able to identify applications traversing ur network and manage whether that application should be allowed or not allowed on your network. Most firewalls also have an additional functionality, for example its common to see firewalls that will allow us to encrypt traffic traversing the network through use of a VPN. Its very common to have a firewall at one remote site and a firewall at another remote site and be able to create a encrypted tunnel between those sites with those firewall using the VPN capabilities. Most firewalls can also operate as a layer 3 device meaning the firewall itself can act as a router. That's because there often sitting right between the ingress and egress point of your network where all the traffic on the inside of the network is going to the outside or internet connection and all the internet traffic is coming inbound. We rely on the firewall to be able to manage communication between the inside and outside of the network. To be able to perform this functionality mini firewalls also provide Network Address Translation or (NAT) and because they are a router its common to have dynamic routing protocols supported in the firewall as well. 


IDS and IPS:
Intrusion Detection system And Intrusion prevention system
Many datacenters may also have standalone IDS or IPS devices but a lot of this functionality is now integrated into the more modern NGFW.  Both of these work in similar ways, they are looking for attacks inbound to your network and are able to identify, alert and in many cases prevent that attack from gaining access to my network. These might Include Exploits against operating systems, vulnerable applications, Buffer overflows, Cross site scripting and more. 
IDS only alert when they find an Attack 
IPS can actually stop or prevent an attack before it gets to the network.



Load Balancer:
 Helps manage Multiple servers for big companies that have alot of people using it they need multiple servers the Load balancer helps balance the amount of data sent to each server and deal with if a server has a outage, helps data redundancy, these load balancers can also act as an SSL offload which means that they will provide encryption/Decryption capabilities. Data may also be cached on the load balancer. Helps with QoS (quality of service)



Proxies:
Proxys sit between the user and the external network 
Proxies are responsible for receiving the users request and then sending the request to the internet
This is useful for caching information, Access control, URL filtering and content scanning. Some applications may need to know how to use the proxy (explict)
but some proxys are invisble and will be used no matter what (transparent)



Network Attached Storage (NAS):
This connect a shared storage device across the network, where any user on the network can access this storage device assuming they have permission.
we will have to download the entire file just to edit one little part of it.

Storage Area Network (SAN) 
This looks and feels like a local storage device with block level access which means we can just change the blocks that were modified, with a very large file this is a good way to modify just a little bit of information within that very large document

Whether using a NAS or a SAN you are probably using alot of bandwidth its common to put the NAS or the SAN on its own network.


Access Point( AP)

This is not a wireless router a wireless router is a router and an access point in a single device.

An AP allows us to communicate wirelessly from our device to the rest of the network , Many routers at home are Actually Routers + AP + a switch in the same device. When in larger enterprise networks your usually using a device purpose built for a single function. Having an Access point means we are using it for wireless communication and wireless communication only.
An access point is a bridge, Commonly on the other side of the access point is a ethernet cable so this is bridging communication between the wireless network and the Wired Eth0 Network This is why we refer to Access points as an OSI layer 2 device or data link layer device because its making that translation between the 802.11 wireless Network and the 802.3 Ethernet network. 

In a large building we will need to have many AP to cover the Needed wireless capabilites of the network, we need to make sure these AP's have proper security controls and are also seamless to transfer from using one access point to another. Seamless network access should be easy 


Wireless LAN controllers:

Instead of connected to each individual Access point to make configuration changes or manage this process we can have a centralized management tool that allows us to manage all of our access point from one central place this is a Wireless LAN controller.
From this single device we should be able to Deploy new access point
We can do  Performance and Security Monitoring from here
We can Configure and Deploy changes to all of our access point on our sites
And to report On access point use and see if we need to update or change any of our AP locations These are usually propertary systems so if we are using an AP from one manafacturer we also are using there Wireless LAN controller.