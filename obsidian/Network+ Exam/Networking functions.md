If you were able to actually get into the network cable and see whats going back and forth between that connection you would see that there is alot of stuff happening behind the scene and there's alot of different stuff going on. 


Content Delivery Network (CDN)

It takes time to get data from a far away place to another a CDN is helped design to speed up this process. these are often Geographically distributed caching servers, so there might be a CDN server in each continent. If you are using youtube you are using a CDN right now.



Virtual Private network (VPN):
This is a secure encrypted tunnel that allows you to connect to a remote network in a very secure and encrypted way.
Vpns often use a device called an concentrator or the Head-end device to be the central connection point for all of the users that are accessing that vpn, this is often a purpose built appliance that is built to handle high speed encryption and decryption of network data in real time so you can have many people send secure data on a network.  This can be a standalone device but Very often we Mix this VPN/Concentrator within a NGFW itself. 
Because of the Encryption/Decryption process required to perform this VPN configuration we will often use a purpose built appliance or piece of hardware to be able to do this. That provides high Throughput, but with a smaller network u really dont need this there are many VPN clients that can run as software on a existing system. This is often used with their own VPN client software but there is some that are built into an operating system


Quality of Service (QoS):
Not all applications are Designed to run simultaneously on a network and some applications may have a higher priority then other applications. For example there may be a Realtime audio/ video feed that has a higher priority then a file transfer. Because of this its very common for network Administrators to provide some type of Prioritization to these applications. This is often done through a Quality of Service or QoS configuration. You may also refer to this as Traffic shaping or Packet Shaping 
This allows the administrator to control what type of applications can flow through there network typically controlled by bandwidth usage or data rates.
This allows you to set important applications with higher priorities then other less important apps. In order to Manage the QoS you may have to configure a Router, a Switch or a firewall . These devices may have prebuilt list of applications, they may also let you add your own application from the list. From that point you can decide what priority the applications might have relative to everything else running on the network



Time to Live (TTL):
One of the problems that we have with technology is that it is really good at performing a task and often it can perform these tasks over and over again without any type of human intervention. Unfortunately this can also put a device into a state where its performing the task over and over and over again and never finds a way to complete or end that particular task. For this reason we have built in different functions with our protocols so that we can recognize when a task may be going on too long and simply remove that task from our network. One way to perform this is through the use of a Time to live or TTL. A TTL is some type of timer, this timer may be based on the time of day or it may be based on the number of iterations that a particular task completes. Once that timer hits 0 we can then have that task stop what its doing or we can drop that task from the network.
There are many different uses for a TTL one is a packet that is constantly looping between routers we may want to have that packet auto dropped if the loop occurs a certain number of times.
another good example of a TTL is to clear a cache, we may access a website have that website stored in the cache and then that cache is only available for a certain number of time or till the TTL hits 0 .


Routing Loops:
Another example of using a time to live to stop traffic that is looping around your network is through the use of a Routing loop. This is an example where Router A thinks the next hop is to Router B and Router B thinks the next hop is to Router A and if this happens then the packet will go back in forth between these routers Over and Over again, UNLESS stopped if you were to perform a tracert you would see the loop in the tracert hops itself. This may happen on accident its very easy to misconfigure.
For routing Loops we use a TTL field inside of the IP packet itself this allows to identify and stop a loop automatically if one occurs.

IP (internet Protocol):
We built function Into IP that will look for a routing Loop to occur and stop it if it finds that it is occurring over and over again. In the context of IP the Time to live (TTL) is referring to the number of hops that a packet will go through a router with each router it goes through being a hop and each hop decreasing the TTL by 1 and when the TTL reaches 0 it discards the packet. The default TTL for MACOS/LINUX is 64 hops and the TTL for windows is 128 hops. a TTL of zero is dropped by the router.


DNS (domain Name system)
In DNS the TTL is associated with the total number of seconds. Lets take a scenario where we are performing a DNS lookup (you can do this yourself by doing nslookup or dig)
The TTL is the amount of time that the Cache of the results of the nslookup or dig scan is saved/ cached on our local systen 