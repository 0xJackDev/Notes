

PDU (protocol Data unit)
These are also referred to as transmission units every layer of the OSI model has a different name for its PDU but all of the PDU are just data thats being sent across the network. Different PDU's operate in different ways for example. Ethernet Operates on a frame of data and it doesn't matter what is inside the data. While IP operates on a packet of data inside is TCP or UDP data for IP doesnt rlly care. And where there is a TCP or UDP header there will be either a TCP segment or a UDP diagram.



Encapsulation and decapsulation:

 Lets start with saying that an application needs to send Data from the web server from the web client That application data exists at Layer 7, 6 and 5. To be able to Transport this data across the network using the TCP protocol protocol so we will put a TCP header right in front of the Application data and use that to send it across OSI layer 4 or transport layer. We also have to have an IP address to be able to send this TCP data and application data that is inside of it so we need to add an IP header so we can send data from one IP address to another. And lasty over we need to add a DLC or Data link control, Layer 2 frame header for Ethernet in many cases you will also add a Frame trailer at the end of the packet to indicate the end of the frame. the layer two frame header encapsulates all of the Data so inside will be the IP header, TCP header, and the application data![[Screenshot 2024-06-24 211203.png]]

Lets expand this view to see both the sending and receiving device and view the way the network may interact with all of this.

Encapsulation is the example of above where you add headers


So say we want to get data across the network. first the Source will start by encapsulating the data and sending it across the Network to the Destination device. The destination device needs to application data that's inside but it doesnt need the Ip header, Frame header or Tcp header anymore. So it will begin removing these headers in a process that is called decapsulation and moving the data up from the OSI model to now have application data again.


Within each OSI layer there is different Header and payload in the header. for example in the TCP Header there is TCP flags, these flags control important control information. Hence why we call these control flags. 
If the SYN flag is set that means there's a synchronization of sequenced numbers that is occurring
if the Push flag or PSH flag is occurring that means the data is being pushed to the application without anything else that might be incoming 
There is also a reset flag or RST which resets the connection 
and a FIN flag that says this is the last or Final packet from the sender 




Maximum Transmission Unit (MTU)
Not only are there flags inside the TCP header but there is also flags inside of the IP header, Most of the flags being used in the Ip header deal with the fragmentation of data . There may be times where you wanna send data across the network but because of the design of the network ur not able to send large packets. In those cases you may need to fragment the data in order to get these packets across the network. we determine the Max size you are able to send using something called the Maximum Transmission Unit or MTU. This designates the size of the data we are able to send through the network without needed to fragment that data anymore. The reason we dont wanna fragment is that is commonly slows down the overall flow of traffic and if you can optimize your network communication so that you never fragment you will have a much higher throughput of traffic. This is why it is important to know the MTU value that would be used all the way through the network from the beginning to the end. 
Sometimes it may be a very complicated process to figure out what the MTU actually is as there may be many different hops used to communicate from Point A to point B and each one of those hops may be using a different MTU. There is a automated process that your system used to attempt to determine what the MTU is when communicating to that other device. but unfortunately if ICMP is filtered in that communication then theres no way to automate that process which means you will have to manually set the MTU on your side. Lets take a look at what this fragmentation really means..


Building an ethernet frame.


The size of our packet is the amount of bytes from the Start of the IP header to the end of the Tcp data. the Ip packet size does not include the DLC header or tail. The maximum size of an IP packet on an ethernet network is 1500 bytes if there is no fragmentation on the network you will be able to send that much data through the network without it being fragmented.


What is Ip fragmentation?

Lets take an example in which we can only send a very small amount of data through the network in this case 16 bytes is the maximum Translation unit supported on this network. That means we might have 44 bytes of data that needs to be fragmented. So if we are going to do this, we are going to fragment it by sending the first 16 bytes of data, then we will send another frame that has another 16 bytes and then the last frame is going to send the remaining amount of data up to 16 bytes. ![[Screenshot 2024-06-24 213052.png]]


Troubleshooting MTU 

Fortunately when you are designing and creating a network the MTU is usually made in the process, so once a network is built its very unusual for that MTU to change. We also know that there is going to be MTU changes if we have to tunnel any information so if you are using a VPN of any type you are probably going to need to set some MTU or ensure that the MTU is going to be properly set.

What if you send packets with the Don't fragment (DF) flag set?:
routers will respond back and tell you to fragment, very commonly you will receive a ICMP message that 