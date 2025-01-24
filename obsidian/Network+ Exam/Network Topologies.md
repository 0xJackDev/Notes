
These are useful in planning a new network. A network topology is the physical layout of a network.


Star Network: 
One of the most popular Network Topologies also commonly referred to as a Hub and spoke where the Hub is in the middle and the spokes are around the outside. This is a topology you will find on almost any network regardless of the size of the network. You will also find that most devices are connecting back to the central hub of the star. For example,  a switched ethernet network has the ethernet switch in the middle of this star and then all of the devices run directly back into that particular switch. They arent connecting to each other they are instead connecting back to the central switch in the Network topology![[Screenshot 2024-06-25 215610.png]]



Ring Network:
Although we don't often see a Ring topology used on a Local area network, it is still a topology type that is used quite often for Wide area Network (WANS).  Still many Metro Area Networks (MANs) and WANs use them quite often, this isnt really a case of that it works better on a Wide area network its because we can create additional redundancy using the ring topology. For example a very common way to send traffic over a ring network is to have the traffic simply go in a circle. Now if we are on this Wide area network and there is construction going on and someone happens to cut a fiber connection thats being used for this MAN, then we wont be able to send that traffic through the rest of the ring. But the devices on either side of that severed link will recognize that traffic is no longer able to traverse the connection and instead will loopback the connection on those individual endpoints, so instead of having data go around a ring the data will instead go as far as it can around the ring and the loopback around the other way to get to the other side of the ring ![[Screenshot 2024-06-25 220145.png]]



Bus Network:

Early type of ethernet networks were not switched ethernet but instead were run over coax. and this coax was quite simply a cable that was run down the middle of a room very similar to the cable in the picture. This is a bus network, and although used in old ethernet networks we can still find modern networks that use the same bus topology. One problem with bus networks is that it is a single cable that is running either through the walls or down the center of the room, and if there is a break into the cable then it would essentially segment the network into different pieces or in some cases cause no data to be transported across the network. This is one reason we Went away from bus network in our LANs. In our modern automobiles we have Bus networks that we use extensively called Controller Area network or CAN bus connection and they are used to connect all of the controllers and sensors in our cars together ![[Screenshot 2024-06-25 220804.png]]



Mesh Network:
Another popular network topology especially in larger networks is to create a mesh between devices or a mesh between sites, we may have devices that are connected in different locations and we might want to connect them all together, but instead of having a single connection to a particular site we may want to create multiple connections to mesh these together. That way if we do lose any one of these network links we are able to work around that problem but simply using another one of the redundant connections, You will commonly use this type of mesh design. The most common place to see a mesh network is over a wide area network where you can create multiple links to other sites, so you can have a primary connection from one site to another then a backup or secondary connection ![[Screenshot 2024-06-25 221127.png]]




Hybrid Network:
When you start combining these network topology's together you create a hybrid network, a hybrid network is more then one of these network types all working together



Wireless Topologies:

If you are using an wireless access point then you are probably communicating over an infrastructure connection meaning all of the devices on your network are communicating through an access point, this is the most common way to use wireless connections but not the only way.

If you only have two devices are there is no access point  that you can use, you can connection from one device directly to another using ad hoc networking.

And if you have added Internet of things or IOT devices then your probably using a MESH network where all of these devices on the network can communicate to all of the other devices simultanealsly  making an interconnected mesh between all of these IOT devices. it allows many devices to communicate to each other even if they are all apart this adds redudancy too.