

THe OSI model (Open system Interconnection) defines a framework through which networking protocols (or protocol suites) can be implemented/ The OSI model consists of seven layers. Each layer has its own responsibility within the communication process. Hosts that have data to send over the network pass the data through each of the seven layers, starting at the top until the last layer is reached. Each layer adds the information it needs to the data in a process known as encapsulation. The information at that layer. As the data is manipluated at each layer, a new name is given to it, as to assosiate it with that specific layer. These new data pieces are called Protocol Data Units or (PDUs). The seven layers of the OSI model and each PDU assosiated is below


Once the data has reached the physical layer of the OSI model it is transmitted onto the networking media and sent to the destination host. The destination host passes the data back up through the layers of the OSI model with each layer processing and removing its header. The process is known as de-encapsulation. This process continues up the layers of the OSI model until the receiving hosts application processes the data. 

![[Pasted image 20240613101850.jpg]]


The Osi model has multiple protocols at the transport layer. In the TCP/IP model there are two protcols that reside at the transport layer, TCP and UDP. TCP and UDP are the most widely referenced transport protocols in the OSI and most of the TCP and UDP functions map to the OSI transport layer. TCP and UDP use port numbers to differentiate between application transmissions. IANA uses RFC 6335 to describe the procedures for assigning port numbers. The tcp protocol is responisble for connection oriented data transmission. TCP converstations always start with a three way handshake this process prepares both the server providing the information and the client receiving the information for the communication. TCP also uses acknowledgments to verify data transmission. The UDP protocol is responsible for connectionless data transmission. UDP only sends data -- it does not send acknowledgments to verify data transmission. This layer is also responsible for breaking down large data into smaller more manageable pieces. This process for TCP is known as segmentation. With UDP the more manageable pieces are called datagrams and have no sequencing information included. THE PDU assosicated with the transport layer of the OSI model is a segment for TCP and datagram for UDP.


FOR A TCP PACKET THREE WAY HANDSHAKE

First packet 

Notice the line Source Port. This port is a randomly generated number between 49152-65535 that the requesting client will use to keep track of this web page request. This range of ports is known as Dynamic Ports.

Notice the line Destination Port. Port 80, the destination port of this packet, is assigned by IANA specifically for the HTTP protocol. Ports that fall into the range 0-1023 are known as System Ports. Some texts also refer to this range as Well Known Ports. These ports are assigned to specific applications allowing the receiving server to identify the application. In this example port 80 indicates that the web server application needs to respond to the request.

Notice the line Sequence Number. Sequence numbers are used to keep all of the TCP segments in the correct order. The first segment in the TCP threeway handshake is always assigned sequence number 0 in a default Wireshark configuration. This segment is called the SYN segment.

NEXT TCP PACKET *RESPONSE*

Notice the lines Source port and Destination port. You will see that the same port numbers are being used, but they have now changed positions. This is because this segment is a response from the server hosting the web page to the web client that requested the webpage. Because the application receiving the response is also a web-based application the port number indicates the HTTP protocol in the returning packet to alert the client to use the web browser.

. Notice the line Sequence Number. Since this is the first segment coming from the server (and the second part of the three-way handshake), this sequence number is also set to 0.

Notice the line Acknowledgment number. The TCP protocol uses acknowledgment numbers to indicate to the client that it has received its request and is responding to that request. The client in turn needs to use that acknowledgement number as the next sequence number because the server expects to see in the conversation. With the exception of the threeway handshake, acknowledgments are not sent for each segment. Instead, they are sent at periodic intervals set by a sliding window. This allows for greater efficiency since a large group of segments can be acknowledged at the same time. In this part of the three-way handshake, the acknowledgment number is 1.

Expand the + next to Flags. Flags are used to set certain options available to the segment. In this example, there are two flags set – the Acknowledgment flag and the Syn flag.

Expand the + next to the line Syn: Set. Notice the line Expert Info. The purpose of this flag is explained. The SYN+ACK segment is used to acknowledge the request for a connection from the client to the serve

Notice the line Window size value. This is the number of segments that will be sent before an acknowledgment is expected. It is called a sliding window because this value can change based upon varying network conditions


LAST PACKET 


. Notice the lines Source port and Destination port. You will see that the port numbers have returned to their original configuration. This is because this segment is the final response of the three-way handshake from the client to the server hosting the web page.

Notice the line Sequence Number. Since this is the second segment coming from the client (and the third part of the three-way handshake), this sequence number is set to 1. This number also matches the acknowledgment number from the previous segment because the server is expecting to see segment number 1 next.

Notice the line Acknowledgment number. This number is also set to 1. The client is telling the web server that is did receive the initial segment and that it is expecting to see segment number 1 next.

Goings down to flags the Only flag set is the Acknowledgment flag

Scroll down and expand the + next to the line SEQ/ACK analysis. This section actually tells you that this segment is an acknowledgment to the segment in frame number 8. It also includes the Round Trip Time, or how long it took for the acknowledgment to arrive.

Once the TCP three-way handshake is complete, data transmission can begin. (These are the segments we skipped earlier.) These packets actually contain the data that makes up the picture on the web page.






Scroll slowly down through the top capture window, noticing the packets that are highlighted in black starting with packet number 15 and ending with packet number 202. Look closely at the Info column. Notice that each of these segments is an acknowledgment to a previous group of segments. Remember that the Ack number is always the next segment expected in the sequence. Notice that even though the Ack number continues to increase, the Seq (Sequence) number does not. This is because the client computer has not sent any additional segments; it is only receiving segments from the web server.


Scroll through the top capture window and select packet number 204 by clicking on it. Notice that the protocol is once again HTTP. In the middle pane of the capture window, expand the + next to [128 Reassembled TCP Segments. This shows all of the packets in the capture that it took to transmit the picture from the web server to the client.


Conclusion:

There are two protocols in the TCP/IP suite that reside at teh transport layer of the OSI model -- TCP and UDP. The tcp protocol is the transport layer protocol used by the HTTP protocol for reliable data transfer. TCP uses a three way handshake to initiate a conversation then sequence and acknowledgment numbers to keep segments in the correct order during transmission. Port numbers are used to differentiate conversations.







Network layer

The network layer of the OSI model is responsible for logical addressing. These addresses are used by routers to move packets between networks. The major protocol of the TCP/IP suite that resides at this layer is the Internet Protocol or IP. There are currently two version of IP which is Ipv6 and Ipv4. Ipv4 addresses are 32 bits in length while Ipv6 addresses are 128 bits in length. And represented by groups of four hexadecimal digits each. 



The Differentiated Services Field can be used to specify certain Quality of Service parameters for a packet. In this example, this field is not used and set to 0x00. 5. Notice the line Total Length. This describes the length of the IP header plus the length of the segment passed down from the transport layer (in bytes). In this example, the total length of this packet is 121 bytes.
The Identification line is a 16-bit number used to uniquely identify the IP packet within the conversation. In this example, the Identification number is 0x0391. The “0x” means that the number being represented is actually in the hexadecimal format. The number in the parenthesis to the right is that same hexadecimal number converted to decimal format. 7. 

The Flags and Fragment offset lines go together. These fields control whether a router can fragment an IP packet and indicate the parts of the packet to the receiver. In this example, the Don’t Fragment flag is set and, as such, the Fragment offset is set to 0.



Notice the line Time to live. This number represents the number of hops (routers) that the packet can go through on its way to the destination. Each router along the way will decrease this number by one. If this number ever reaches “0” (typically due to a routing loop) the packet will be discarded. In this example, the TTL is set to 127.


The Header checksum is used to verify that the header has not become corrupted or modified in transfer. If the checksum is correct, the packet is accepted. If the checksum is incorrect, the packet is discarded. IP is a connectionless protocol meaning that if it discards a packet, it does not ask for the packet to be retransmitted. In this example, the checksum was calculated correctly.


Notice the lines Source and Destination. These represent the logical IP addresses of the client and the server. In this example, the Source IP address is the web server (131.107.0.200) and the Destination IP address is the client requesting the web page (192.168.12.11).




5. Reviewing Data link layer
Organisational Unique Identifier

The first half of any MAC address is referred to as **the OUI, or Organisational Unique Identifier**; this arrangement of characters are unique to a particular manufacturer and can be used to identify the manufacturer simply by looking at these characters.

The data link layer of the OSI model is responsible for physical addressing. These addresses are used by devices such as switches to move frames between nodes on the same network. One of the most common protocols that reside at this layer of the OSI model is Ethernet. Ethernet uses Media Access Control, or MAC, addresses burned into the ROM of network cards (NIC) to address its frames. MAC addresses are 48 bits, or 6 bytes, in length and are unique to every NIC. The PDU associated with the data link layer of the OSI model is the frame.
Notice the lines Destination and Source. Ethernet uses the physical MAC addresses burned into the NIC as the addresses at this layer.

The Destination address in this example is the MAC address of the client machine (look at the one in parenthesis). The first 3 bytes of the MAC address represent the Organizationally Unique Identifier (OUI). This is a number assigned by IEEE to identify the vendor of the NIC. Wireshark automatically substitutes the vendor’s name for the first 3 bytes of the MAC address. The last 3 bytes of the MAC address is essentially a serial number assigned to the NIC by the manufacturer




6 Reviewing the Physical Layer

The physical layer of the OSI model incorporates all of the tangible network components such as cables, connectors and repeaters. The electronic signals on the media are also included in this layer. The electronic signals make the 1’s and 0’s that physically represent the data on the media. The PDU associated with the physical layer of the OSI model is simply bits.


The physical layer of the OSI model incorporates all of the tangible network components such as cables, connectors and repeaters. The electronic signals on the media are also included in this layer. The electronic signals make the 1’s and 0’s that physically represent the data on the media. The PDU associated with the physical layer of the OSI model is simply bits.