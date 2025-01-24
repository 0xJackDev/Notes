While IPv4 Deals with 32 bit Addresses



Internet Protocol Version 6 - This is a 128-bit Address protocol.
There is about 340 undecillion different possible IPv6 addresses Which is ALOT.

IPv6 though looks alot different then ipv4 this is what is looks like in binary ![[Screenshot 2024-07-12 185335.png]]

And we tend to write ipv6 has hexadecimal values 

There is 2 bytes Or two octets in the Typical Ipv6 group 

There are ways to write ipv6 address shorter 


Since IPv6 addresses are so large we dont tend to Memorize them we use a DNS SERVER



Ipv6 Compression:

If there are groups of zeros you can abbreviate all that groups and replace them with a double colon :, One one set of Colons is allowed but thats a easy way to get rid of alot of zeros. You can also get rid of any leading Zeros in a group. 
for example to compress the address
2600:DDDD:1111:0001:0000:0000:0000:0000:0001
We can remove All the leading zeros so.
2600:DDDD:1111:   1:   0:   0:  0:     1
We can abbreviate 2+ groups of Zero with Double colons so we can make it now 
2600:DDDD:1111:    1::                    1

Geting rid of all the zeros that are together into a pair of ::



Just as we use DHCP with ipv4 We could use DHCP with IPV6 but we created methods within IPv6 allowing you to statically assign a IP address within using a DHCP server this is done by modifying the MAC address of this device to what is called a EUI-64. The MAC address never changes on our computer Extended Unique Identifier (64 Bit) EUI-64.

Effectivley we are going to create a Combined version of our mac address with a 64-bit Ipv6 prefix to create a new IPv6 address. 

The MAC address is only 48 bits long so we add Data to the middle of it. 


THE MAC ADDRESS 
This is the ethernet Medica Access control address, also refered to as a EUI-48 address this is the physical address of a network adapter.

The mac address is split into two parts, the first part is called the OUI or Organization Unique Identifier (OUI) This is Specific to what manufacturer made your network card You can think of this as the manufacters serial number. 
The last Three bytes are the Network Interface Controller-specific value. This is what make your card unique to the Organization who sold it to you, it should be a unique value for every particular piece of hardware.



The way we Turn the EUI-48 into the EUI-64 is by:
first we wplit the MAC address into the two 3 byte halves, We then add the Values FFFE in the Middle which acts as the Missing 16 bits, 
When we do this we have to make a slight change to the existing mac address, thats because we are changing this from something thats globally unique into something we created, Effectivley you are creating the Burned-in address (BIA) into a locally administered address, this is the U/L bit (universal/Local )




To be able to convert between a Universal address and somehow define that this address is something we have configured we change a single bit within the mac address, And that single Bit is the Seventh Bit inside the MAC address so say you have 11111111 it would turn into 11111101 while 11111101 would turn into 11111111.



With Ipv6 The first half of the IPv6 address is usually associated with your Ipv6 subnet Which is 



The process of flipping the 7th bit Can be annoying. ![[Screenshot 2024-07-12 201124.png]]

Heres a chart to know what hexadecimal digit to flip the First byte 2nd hex letter to If its 0 flip to 2 if 2 flip to 0 so on so forth ![[Screenshot 2024-07-12 201237.png]]