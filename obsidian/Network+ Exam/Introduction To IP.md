The data networks we created allow us to move a large amount of data from one point to another 



There is a very simple Process that happens when moving data from point A to B



If we were to look at the way IP operates we would start with the very Basics of an ethernet Frame. With an ethernet Frame, in this case one thats communicating with a client and a server we have an ethernet Header an Ethernet Trailer, and inside That header and Trailer is the entire Ethernet Payload, Inside that Ethernet Payload Is gonna be IP and The IP Header and the IP payload, The IP payload of course is Usually filled with TCP or UDP DATA, in this case TCP so it has TCP header and TCP payload, And inside of TCP there is Some type of data, in this case a web server so it has HTTP traffic ![[Screenshot 2024-07-13 000853.png]]



Generally there are two ways to move data from place to place either TCP or UDP, We sometimes refer to TCP or UDP to a Layer 4 protocol.

By using TCP and UDP inside of this we are able to perform 

Multiplexing:
which means we can communicate using multiple applications simultaneously over a network while using these different types of protocols 




TCP stans for Transmission control Protocol:

This is connection-oriented with a formal connection and setup, 

This is reliable Delivery This is because of the Three-way handshake in the beginning it makes sure the data can be delivered before sending it. 
We also add sequence numbers inside this TCP header so incase the packets get out of order we can put them back together on the other side or if we are missing a particular packet we will know, and request Just that packet to be retransmitted

The receiver can mange the traffic flow by sending specific acknowledgement information to tell the Sender to either slow down traffic or speed up 




UDP Stands for User Datagram Protocol:

UDP is much more straightforward, it simply sends Data from one device to another there is no process of setting up the connection prior to sending the data, and there are no acknowledgements sent back from the receiving device to confirm that the data has been received, 

When you hear UDP referred to as an unreliable delivery, that doesn't mean the data somehow doesn't make it across the network its because we don't receive any type of acknowledgment when that data is sent across the network, there is no reordering of data or retransmission 

No flow Control




Once a packet arrives we use port Number to designate where the data will be delivered, A port number is referring to a location of a service on that device, so for a web app 80 or 443. and that data is handed off to that Port Number/ That application running under that port.


Sometimes you will see Port numbers and Ip addresses Combined together into a single series of numbers we commonly refer to this as a socket, For example the a socket consists of A IP address, Protocol(tcp/udp), and a port number for both client and server.


The port numbers we use when dropping this data off is often a well known number, they are often a permanent value that is always associated with this service, we refer to this as

Non-Ephemeral Port: 
Meaning these ports are relatively permanent and is usually something thats very well known, for example on a web service the well-known port numbers.
Ports 0 - 1023 are Non-ephemeral and these are usually associated with a Server or a service. 


Ephemeral ports:
these are temporary ports that are temporarily used often on a client device to be able to communicate with these services these commonly range through 1024 through 65-535





Port Numbers:
these port numbers are really used so we know were to send data it can be any number through 0 and 65,535

UDP ports can only be used for UDP 

TCP ports can only be used for TCP


Most Services Use Non-Ephemeral Port numbers not always though


Port numbers are used for communication only, not security 

Service Port numbers need to be well known



When sending Data over TCP/UDP you need to be able to differentiate from this so Say a server was running both Email, VOIP and a HTTP server it would be important that the server is able to differentiate between the types of data.

We are able to do this using port numbers. For example ![[Screenshot 2024-07-13 003255.png]]















1.1.1.1 



TCP- 
