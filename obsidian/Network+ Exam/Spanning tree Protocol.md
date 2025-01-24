
Loop Protection:
Ipv4 has a TTL where it will identify when a loop has occurred and drop that packet from the network. Unfortunately with OSI layer 2 Ethernet There is not a TTL mechanism. If you have created a loop in the network and a frame in introduced into the loop and a frame has entered that loop the only way to stop it is to physically unplug the cable. The key with Ethernet and Switching is to make sure that a loop doesn't occur in the first place. We do that by using Loop protection
- Its very easy to make a loop in a switch network, all you have to do is accidently plug in two cables in to switches and its a loop
- if you connect two switches together it creates a loop
- easy way to bring down a network
- Hard to troubleshoot
- easy to resolve
- IEE standard 802.1D to prevent loops in  networks This is spanning Tree Protocol




STP port states:
When an interface is connected to a network, spanning tree begins the process of identifying whether a loop would be created with that interface or not. And there is a number of modes that the interface will be placed in.

those port states is 
- Blocking port state. This occurs with STP determines a loop would be created by turning on this interface. This will stop all traffic from going in or out of the interface 
- Listening port state. This is what STP uses in order to determine if or not to Block the port state. It needs to listen for a certain amount of time to be able to know what devices and switches are already on the network. In this state STP will not be forwarding traffic and it will begin cleaning the MAC table.
- Learning port state. during this process STP begins building its own internal topology to understand if a loop is gonna happen. During this It is not forwarding data, and it is adding data to the MAC table.
- Forwarding port state, During this the Switch will act completely normal and all data will be forwarded 
- Disabled port state, This is not part of STP process but you as the admin can disable a port with STP




There are three separate modes we are gonna need to know for all of the bridges/switches. 
- root port, This port designates the port that is closet to what we call the root of the network. And only one switch is the root switch.  There is also a root port on each switch. The root port on the switch is always gonna be the one closest to the Root Switch
- Designated Port, These are all the other operational ports on every other bridge/switch.
- Blocked ports, This is Ports that have been BLOCKED  off because STP has identified if they are open it will cause a loop will occur if it open
- 
![[Screenshot 2024-07-16 032024.png]]




One of the challenges with original STP is that convergence process can take along time in listening to see if it will be blocked it can take up to 50 seconds we created a new version of STP called 

RSTP (802.1w standard) Rapid Spanning tree Protocol:
Makes convergence time 6 seconds. 
- Same thing as STP really.