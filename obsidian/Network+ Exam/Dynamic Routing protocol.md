When surfing websites we often dont think of the process to get info from our computer to that remote web server then back again. 

This process is handles by a series of routers on the internet, and each one of the routers knows exactly where your traffic should be going at every hop. 

It can do this thanks to a series of routing tables within the router, and one common way to update that routing table is through the use of Dynamic routing protocols. 

The way most routing protocols works is they perform a listening process, where they determine what other routers may be located near them. They will then build a table within the router and send their own advertisements to routers that are nearby. These advertisements allow routers to work together to build a series of routing tables.

Those routing tables are used by the router to determine the best path for traffic to be forwarded. 

Theres many different dynamic Routing protocols and each one is different 


When network changes occur, update the avaible routes and work around outages




The answer to the question of which routing protocol to use is It depends What the route is.





Distance-vector routing protocols:
these are protocols that will determine the Best route based on how far away the particular connection is.  The Closest Possible Router will almost always be used. 

The process for configuring a Distance-vector protocol is Usually automatic with very little configuration on most routers you simply enable to protocol

- RIP (Routing Information Protocol)
- EIGRP (Enhanced Interior Gateway routing protocol) common with cisco








Link-state routing Protocol:
Information passed between routers is related to current connectivity

Link-state protocol the status of the network is what determines whether traffic can flow across the connection. If the network is up and running You can send traffic over that link. If theres a connection with little or no bandwidth we wouldnt send data over that.

Many link-state also consider the speed and always will choose the networks even if it makes you take additional hops

- scalable 

- OSPF (Open shortest Path first) scalable Protocol used on large networks









Hybrid Routing:

Theres advantages to Link-state and Distance-vector but if you could combine these it could be better. There are some of these but not many A good example of this is

BGP (Border gateway Protocol) 
- determines route based on paths, network polices, or configuration rule sets this is a very common protocol 