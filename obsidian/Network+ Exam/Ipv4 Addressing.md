

If you are configuring IPv4 on a computer then you need to configure three important addresses

The first Address is an IP address this is an address that uniquely identifies this device on the network. so for example 192.168.1.165 would be an example of an Private IP address that no one else on ur network has. This is how other devices will address of send information 


The second Important configuration setting is the Subnet mask, This is a mask that is commonly looks like  255.255.255.0. This is a number that is used in conjunction with your IP so that your device understands what IP subnet it happens to live on. This is important when you are trying to route outside your local IP subnet. And you need to send information to a default gateway, if your ip doesn't know what subnet its on then it doesn't know what data should be communicated locally and what info should be send to your default gateway, so make sure you configure your subnet mask so your device knows exactly where this data should be sent.


An ip subnet is a segmented part of a larger network. 




The third configuration that you will have to set is that Default Gateway address. This is an IP address that is on the same Local subnet as your IP address, this is where your gonna be sending all of the traffic that needs to go outside of this local subnet. 

If configuring your settings and you ask someone for the Local gateway they will provide you with the default Gateway IP 

You will also very commonly configure an additional setting that's not listed here for your DNS server. 


On my computer this is what those 3 look like
   IPv4 Address. . . . . . . . . . . : 192.168.86.40
   Subnet Mask . . . . . . . . . . . : 255.255.255.0
   Default Gateway . . . . . . . . . : 192.168.86.1






Special IPv4 Addresses

Loopback Address:
This is an address that references itself, meaning if you send any traffic to a loopback address, You are really just sending that to your Local machine. The ranges for this Loopback address is 127.0.0.1 through 127.255.255.254, but commonly the easiest way to reference it is with 127.0.0.1, THIS IS ALSO CALLED LOCALHOST. 
This loopback address is a good way to determine if the IP stack in your machine is working properly, You can perform ping 127.0.0.1 and if you get a response from your machine that means that the IP stack is working properly. If you ping 127.0.0.1 and get no response then there is a problem within the TCP/IP stack in ur operating system




Reserved Addresses:
there is a block of addresses that have been set aside for future use or testing. these are "reserved Addresses", 
This is a Class E Ip address
Ranges from 240.0.0.1 Through 254.255.255.254
Everyone should understand these addresses should not be used. so you shouldn't ever encounter one. 





Virtual Ip Address (VIP):
This is one special address you may find working with routers or other devices with multiple IP addresses is a Virtual Ip address. A Virtual IP address is one that is assigned internal to your system, but it isnt assigned to a physical network adapter instead its being assigned to a logical network adapter that only exists inside of the software on your system. These Virtual Ip addresses are commonly seen with Virtual Machines and you might also see VIPS used inside of routers so that there is always a Static IP address you can reference for that particular router configuration. 






Lets Breakdown the Internet Protocol version 4 
This is sometimes referredc to as a OSI layer 3 address 


If you are to convert any IP address to binary you will see that an IP address is 4 different bytes, or Octets are separated be.



Since one byte is 8 bits the maximum decimal value for each byte is 255.

Ipv4 is made of 4 bytes/ Octettes so 32 Bits.




DHCP (Dynamic Host Control Protocol):
IPv4 used to be a manual process but that changed now,
There are many devices  on your network that have been automatically assigned an  , A subnet mask, a gateway, A dns Server, NTP servers, etc. For devices on your network This is because of Windows Dynamic Host Configuration Protocol which provides automatic. This protocol takes a system that has not been configured with an IP address. Communicates over this network using this protocol and Automatically assigns IP addresses to devices. This saves alot of time for the network admin 


DHCP is a way of automatically assigning IP addresses on both Home networks and Enterprise network, but there may be times when a DHCP server is not available and you find your device has been assigned an IP address. In that case you were probably assigned a Automatic Private Ip address. This is what we call a link-local address. Because the IP address thats assigned by your computer is not able to communicate outside of your local subnet. If you have been assigned a APIPA address you are not able to communicate out to the internet. This is because routers are not able to forward APIPA addresses

Automatic Private Ip Addressing (APIPA):

One way to tell if you have been assigned an APIPA address is to simply look at the IP address and if the IP address if between the range
169.254.0.1 - 169.254.255.254 
Then it is  an APIPA address 
The standard is actually a little smaller of a range but because the standard for APIPA takes the first and Last 256 addresses and reserves them. So the actual range of IP address that can be assigned to a device is between 
169.254.1.0 - 169.254.254.255


If a DHCP server is not available then this APIPA assignment begins. Your computer picks a random address in range then send an Address Resolution Protocol (ARP) to the network to see if anyone is using the address. If no response then the address is assigned to the computer. 

If you are ever assigned a APIPA address then your probably connected to a network that doesn't have a DHCP server or the DHCP is broken