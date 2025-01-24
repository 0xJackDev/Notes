
Peer-to-Peer

With a peer to peer network, theres not a server or a client instead every device is a server and a client. Meaning everyone is communicating to each other to be able to gain access to the data they might need. 
PROS
-Low cost
-Easy to deploy 
CONS
-Difficult to administer due to the fact the entire application is distributed, all of the authentication process is also distributed so its very difficult to be sure that a peer-to-peer application will remain secure

![[Screenshot 2024-06-25 234848 1.png]]
Client-Server:
With a client server communication the responsibilities are split, there's individual clients and then the centralized server and when clients need to access data everyone will access the same server. As you can see by this diagram Clients are not communicating to each all other All of the clients talk to the server and the server talks to the clients
PROS
- Performance
- -Easy to administrate  
CONS
-Cost
-It can be complex to setup a server and maintain it. 

![[Screenshot 2024-06-25 234902.png]]





LAN:
Local area network.
it is called local because it is usually within the same building that you happen to be in. This could also be the network that's in the same building but between different flows, Local is relative.

Generally speaking A local area network should have high-speed connectivity and will be using ethernet and 802.11 wireless standards. Any slower communications and it isnt a Local area network. 




MAN:
Metropolitan Area network
This is a network in your city, Larger Then a LAN, but often smaller then a WAN
Commonly governments use MANs because they are very geographically dispersed throughout the metro area and they have right of way so its easy for them to put fiber in the ground and connect all of their remote locations



WAN:
Wide area network
If you are going outside the scope of a WAN and communicating over a much larger distant then you are probably using a WAN. One common characteristic that tends to be very common when you start expanding the distance on these networks is that these networks become slower. So Wide area networks wont be as fast as a local area network. 
If you are connecting over an MPLS network or Point to point serial WAN connection then you are certainly communication over a Wide area network. These could be links which are fiber in the ground or could be satellite communication is certainly a wide area network 


WLAN:
Wireless Local area network 
This is a specialize type of LAN that is wireless. 
These use 802.11 Technologies 
This is within a building in a limited geographical area, typically if you leave your building it will stop working. but if you are in a larger area there are ways to extend this distance using multiple access points.



PAN:
Personal Area Network:
This is your own private network for example Bluetooth, IR, NFC. 
If you are in your car and you connect to the speaker of the car that is a PAN or if you connect ur airpods to your phone thats a PAN




CAN
Campus Area Network Or Corporate area network
This is a group of buildings for a university or maybe for Group of office budlings. Common to use LAN technologies like Fiber and High speed ethernet to connect one building to another and connect all of your users together





NAS 
Network Attached Storage
This allows you to connect to a shared storage device across the network so you can either put Files into the NAS or Download files from the NAS
This provides File level access meaning if you wanna change one thing about the file you have to completely download the file and change it and have to be done to the entire file if its an super large file like say a 30 gb file then if you make one little change you have to overwrite the entire 30 gb of the file because you are using Network attached storage, this can take a very long time especially over a slow network/



SAN
Storage Area network
This to your computer looks and feels alot like a local storage device. So you can make block-level changes to these files without having to overwrite the entire file which is very useful when working with large databases, 
very efficient at reading and writing. 
These require a lot of bandwidth and its usually a good idea to have a dedicated network for the storage area networks or NAS's. and you would probably connect  these with the fastest network possible 




MPLS ( Multi Protocol Label switching)  Network (TYPE OF WIDE AREA NETWORK)

Through the years there has been a number of different wide area network techs, we have Frame relay and ATM and as our needs changed and the way we use these networks changed we needed a smarter way to communicate so we created MPLS.

Multiprotocol Label switching This is communicating through the Wide Area Network, but it uses labels to determine how we route and forward that traffic through the WAN. 

One advantage of MPLS is that we can use almost any type of connection for MPLS and we can put almost any type of Data inside of an MPLS network. Meaning we could send IP traffic, Ethernet frames, or any type of data we would like through the MPLS network 

-This is a common WAN technology as it is easy to setup and get running and have all of our data transferred 


MPLS pushing and popping 
with IP routing we are always concerned about IP subnetting and the next hop we are gonna make. but in MPLS we make forwarding decisions based on the Label switching. This label switching is something thats added when we put information into the MPLS network.

If we have data and we have information on one of the network and we would like that data to get to the other side of the MPLS network,

First we send that data into the first provider edge router thats closest to us. That edge router is then going to insert a label into this data. We call this "Pushing" the label onto that data. Its then going to know how to forward that traffic through the internals of the providers switch network and when this data reaches the other side the label is "popped" off of the communication and the remaining data is sent to the customers router 



mGRE  (TYPE OF WIDE AREA NETWORK)
Multipoint Generic Router Encapsulation 

With MPLS, we have to create an initial configuration that defines where all of the different sites may be located and what labels may be used to switch data to those locations Other types of Wide Area networks could create network connections dynamically so that yours only connecting to those sites when you need to. 
This commonly uses MGRE which is the Multipoint generic Encapsulation and you will usually see networks like a dynamic multipoint VPN or DMVPN used to send data across one of these networks. 
What is nice about these dynamic connections is that they are only created when needed and torn down when you don't need any data you need to send. it can also rebuild itself to be able to communicate to all of these sites. All of this is considered a Dynamic mesh because you send it wherever the data needs to go so you can have two remote sites have a VPN connection between each other without having to go through a central jump point or anything. 



SD-WAN
Software Defined Networking in a Wide Area Network 
This is a WAN that is built for the cloud 
we used to have a datacenter in one building now we have cloud applications so instead of hopping through the datacenter we can have the Wide area network recognize to deliver data directly to the cloud. Software defined Networking in a WAN made Accessing cloud based services over a wide area networking IMMENSLY more efficient as not having go through a data center is a lifesaver 