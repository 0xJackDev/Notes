


Unicast:
If you are using any device connected to the network, most of the communication is gonna be unicast.
Unicast means One device is sending information directly to another device. This is a one-to-one communication between these two devices. 
A Server Request/Response is an example of Unicast communication.
Web surfing, File transfers are probably using Unicast communication

Works great when one device needs to communicate to another but it struggles when a single device needs to communicate to multiple devices at once. 
For example say you have a real-time streaming media Platform, It would have to send a single separate stream to every single device on the network that is using your platform. Which is very inefficient 

Used with IPv4 and Ipv6





Broadcast:

There are more efficient ways to send information to multiple devices on the network at the same time.
One of these ways is to use a Broadcast communication, where one device can send one piece of information And that one piece of information is seen by ALL other devices on the network.

This is an important characteristic of broadcast that the source device is sending out a single packet of data and that single packet is transmitted to every other device on the network. This makes it very efficient communication from the source device because it only needs to send One packet.  Yet everyone on the network can see it. 


Obviously We are not able to send One packet to the internet and somehow communicate with every other device that's on the internet. The range of communication used in a Broadcast is called the Broadcast Domain. And it usually limited to your local IP subnet .


There are many IP protocols that rely on Broadcast to send updates to all of the other devices on the network. Like ARP requests 


One thing about broadcast is that if you have a large number of broadcast communication on the network it can create performance problems for all of the other devices.

In IPv4 We use Broadcast extensively

In ipv6 though we changed this by limiting the scope of what's sent to all of the devices by using multicast instead 






Multicast:
Multicast allows you to send a single frame that would only be seen by devices that are interested in receiving this information, and devices that are not interested are not affected by a multicast. We often see Multicast used for Multimedia communications, Stock Exchanges Updates, and dynamic routing updates.

Because of the specialization required to only send traffic to interested parties this is a technology that doesn't tend to scale with larger networks. It has be very carefully engineered to send Multicasts From one side of the network to another and this is why We don't often see Multicast communication occurring across the internet 



This technology is seen with IPv4 an IPv6 but IPv6 more as IPv6 doesnt has broadcast



![[multicast_946.webp]]




Anycast:
There is another way to communicate where you would have a source device that needs to communicate to a different type of device, and there's multiple nodes on the network but you only need to talk to one of them.  This is anycast Which allows you to communicate to any device on the network but that single device could be one of the many options available 

Used in Ipv4 and Ipv6

If you were to look at the configuration of these devices it would appear to have the same Unicast addresses assigned to them but they are actually anycast addresses and will respond to any request made looking for that particular address. 

This anycast tech is used extensively on the internet. You will have devices that request information via anycast and the closest device will respond back  Allowing you to distribute these servers geographically. This is commonly used with DNS , where there is only 13 devices Defined as Root DNS servers but in relatity there is thousands as we configured them to use anycast and chose the Closet DNS *If you can only add 13 ROOT dns servers in you Config file on ur machine then instead set an ANYCAST address to just choose the cloest https://www.cloudflare.com/learning/dns/what-is-anycast-dns/*