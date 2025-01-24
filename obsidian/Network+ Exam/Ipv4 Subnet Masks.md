
A subnet mask is a contiguous series of 1s all of the 1s are on the left side of the subnet mask and the 0s are on the Right side of the subnet mask this is a Class C subnet mask in binary

11111111.11111111.11111111.00000000

or 255.255.255.0 in decimal

or /24 in CIDR block notation (classless interdomain routing)

you could also use a shortcut to describe this subnet mask by counting the number of 1s and putting that right after the / value so this subnet mask could also be referred to as /24. We refer to using a Slash as the notation as CIDR block notation Stands for Classless Inter-Domain Routing. 

The subnet mask is used to Deletant the Network Part of the IP address from the Host part of the IP address all of the 1s designate the Network Portion while the 0s are the Host portion



11111111.11111111.00000000.00000000 = /16 or = 255.255.0.0


Lets do another Binary to CIDR-Block notation This time not using a subnet mask that doesnt follow the 8 bit octets so lets look at the ip addr 

11111111.11111111.11111111.11000000 = /26

we do the same thing where we just count up the ones so the CIDR block nation for this would be /26. This means that the network portion is 26 bits long and host portion is 6 


One thing we will commonly do when seeing binary subnet masks is try to convert them back to decimal. One easy way to do this is building a chart

11111111.11111111.11111111.11000000

255.255.255.192

![[Screenshot 2024-07-09 010538.png]]

\
