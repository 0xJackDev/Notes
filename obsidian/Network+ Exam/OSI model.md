
Stands for the Open systems Interconnection Reference model. This is a model used in IT to describe the process that data takes as it traverses our networks. The OSI model is not designed to be a detailed description of this data but instead is intended to describe a broad overview of data traverses our system. This is also not the same as the OSI protocol Suite and most OSI protocols didnt catch on it just so happens that the OSI model works perfectly with TCP/IP

There are unique Protocols are every layer that may exist in one layer of the OSI model but not another




[[OSI Layer 7]] is the Application layer
[[OSI layer 6]] is the Presentation Layer 
[[OSI layer 5]] is the Session layer
[[OSI layer 4]] is the Transport layer
[[OSI layer 3]] is the network layer 
[[OSI layer 2]] is the data link layer
[[OSI layer 1]] is the Physical layer


APSTNDP


[[OSI layer 1]] is referred to as the physical layer because its describing the physical signals we send thru the cables and fibers of our network. At this layer there isnt many protocols we are really just talking about getting a signal from one part of the network to another. When we refer to a physical problem with the network we are referring to the OSI Layer 1. 


One step up from the Physical layer is OSI layer 2 the Data link layer.
this is the fundamental layer that is used to communicate between two devices on a network. We often refer to this as the MAC address layer, because that is the Data link control layer or DLC layer that is commonly  associated with the network cards inside of our devices. and most of the time these are Ethernet or Wireless adapters and we refer to the physical mac address on that device as the Data link control address for that device. or MAC address MAC standing for Media access control. Since the network switches that we use on our network determine how to forward traffic based on the destination Mac address, This layer is often referred to as the "switching layer"


The next layer up is Osi Layer 3 or the network layer. We often refer to this as the Routing layer as this is the layer that routers use in order to determine how to forward traffic and they are specifically looking at the destination IP address to determine what the next hop might be for traffic traversing the network. This is also the layer that we're able to fragment these frames into multiple pieces. Especially if sending it across a network that may require smaller frames than what is on our local network.  Anytime we are solving a problem related to Ip addressing, Subnet masks or anything related to an Ip  address or anything about routing, we are refering to Layer 3 probaly.


Layer 4 Is the transport layer and as the name implies we're referring to the ability to transport information from one device to another. You might also refer to this as the post office layer because this is responsible from getting your data or "Letter" from one side of the network to another. The protocol that are often used and operate at Layer 4 of the OSI model. Is TCP(transmission control protocol) , and UDP (user datagram protocol). These protocols are responsible for getting all of the information within our IP packets from one device to the other. In Many cases this involves taking a large amount of data, putting it into smaller pieces to get it across the network then putting them pieces back tg on the other side. 
Before we can send the information from one side to the other we may need to create a session so that the other device is able to receive that data.


Layer 5 is the Session layer and it provides communication management between devices.  Anything relating to the initiation of a session, stopping the session, or restarting the session can commonly be related with layer 5 session behavior. If an application is using some type of control protocol or your tunneling information within existing data then you are probably using OSI layer 5


OSI Layer 6 is responsible for putting all of this data into a format that we will eventually see with our human eyes. This refers to character encoding, Application encryption and decryption, and this is often combined with the Application layer . This is commonly The operator just prior to us seeing the data on our screen. 


The top Layer of the OSI model OSI layer 7 or the application layer. this is the layer that we see on our screen so anytime we are interacting with an application we are operating at layer 7 of the OSI model. Common Applications that run at OSi layer 7 is Https/http. Ftp, POP3, Imap, and thousands of other application protocols.


With that broad overview it may be hard to fit things into the real world 

Starting with Layer 1  the physical layer this refers to cables, fiber, and the electrical signal itself 

When we refer to OSI layer 2 or the Data link layer then we are referring to ethernet frames, Mac Address or Extended Unique Identifiers (EUI) EUI-48 or EUI-64 addressess, or anytime we refer to switches we refer to Layer 2


Layer 3 or Network layer refers to Anything With Ip Addresses, Routers, subnet masks 


Layer 4 or Transport Layer Has anything to do with Tcp Segments or Udp Datagrams


Layer 5 or Session layer has stuff to do with Control protocols and Tunneling protocols 


Layer 6 or Presentation Deals with Application encryption (SSL/TLS)


Layer 7 or Application layer is where u are interacting with the computer urself and u can see it. 