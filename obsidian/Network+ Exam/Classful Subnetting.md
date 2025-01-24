
Learning more about subnetting The process of understanding subnet masks becomes very important, when talking about Ipv4 Subnets you will often hear of differences between Class A, B, and C. 
This is referring to a Very specific subnetting architecture technically not used since 1993 but is still referenced in casual conversion.
When IP was originally created subnet masks were determined automatically based on what ur ip address was. But today we have much more control over our subnet mask because we use what is called Classless Subnetting. For the purpose of understanding todays form of subnetting we are gonna look how are this classful based subnets process works. 


These classes of subnets have a very important application from todays subnetting as  this is the default starting point for subnetting masks. Its important to know when a subnet begins and how much we can subnet from that point. 


There are technically five different classes ![[Screenshot 2024-07-09 003136.png]]


You will commonly see Class A, B and C as that is what we assign to computers. 

If working with Multicast you will work with Class D

Class E addresses are reserved and should never be used 


One way to determine the class of an IP address is to look at the first Octet in the entire address 

Report to the chart about with the Leading bits if they start with those numbers then that means its that Class of subnet 

for example 126.125.125.125 would be a Class A 


If u convert the first OCTET of an IP addr to binary and look at just the First four bits you will find that any thing that starts with a 0 is Class A, Anything that starts with 10 is Class B, 110 Is class C and 1110 Is Class D and all 1s is class E.


When subnet masks were auto configured the Subnet mask was determined on the IP ADDRESS automatically, Refer to chart.


In a Ip address the Host bits are the Portion of the Address that identifies a specific device or host within a network. IP addresses are composed on two parts the Network portion and the Host portion 

The construction of a Subnet

When working with IP subnetting there are four different values you have to calculate which is.


Network Address: 
This is the first IP address that is in a subnet, to calculate this we set all the Host bits in the address to 0 or 0 decimal and we calculate what the decimal value of that might be



First Usable host address:
This is one number higher then the Network address 



Network Broadcast Address:

This is the last ip address in a subnet, In order to calculate this set all the Host bits to one or 255 decimal. 


 Last usable Address:
 This is one number lower then the Broadcast address 


Lets start with an IP address of 10.74.222.11 
This is a Class A address  The default subnet mask for this would be 255.0.0.0 
because we know the subnet mask is 255.0.0.0 we can add a separation in this particular address where all the 255 values are on the left and all of the 0 values are on the left meaning
since 10 is the first octet and the subnet address first octet is 255 we seperate 10 to the left. While the rest of the Subnet Masks Octets = so the rest go to the right leaving on the right

74.222.11 

and on the left is 
10.

THIS MEANS that 10. is the Network Portion of the IP address while, The 74.222.11  is the Host portion so to figure out the network address we will set 74.222.11  to 0.0.0 so the network addr is 
10.0.0.0, meaning the first Usable addr is 
10.0.0.1

The Network Broadcast address would be 
10.255.255.255
and the last usable address would be
10.255.255.254

As long as you know the class and where to put the divding line then it should be easy 


Looking at another ip 

172.16.88.200
Class b Subnet = 255.255.0.0


The Network addr is 172.16.0.0

the First usable addr is 172.16.0.1

the Broadcast addr is 172.16.255.255

the last usable addr is 172.16.255.254



now 192.168.4.77
Subnet mask = 255.255.255.0

Network addr = 192.168.4.0

FIrst usable 192.168.4.1

Broadcast addr = 192.168.4.255

Last usable addr = 192.168.4.254

These days we are able to subnet into any of these octet in future videos we will look at how to do these operations with classless subnetting 