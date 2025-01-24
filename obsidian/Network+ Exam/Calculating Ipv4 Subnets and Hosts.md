
Why the subnet the network. If youve ever seen a network diagram then youve probaly seen a mixture of routers and IP addresses with subnet masks, and each one of these networks is subnetted into its own range of ip addresses. The quesiton is why go thru the process of subnetting?

One of the most common reasons is its very difficult to connect all devices to all other devices in the world simultaneously.


Instead we use routers to separate the network into smaller pieces and we simply send our traffic to the next router who then determines where the next route would be after that. Its a simple way to manage a large number of devices on a network and still allow us to communicate to all of them. 



Prior to 1993, Your subnet mask was set automatically based on what your IP address happened to be. This is a class based subnet method. That we found was not able to be as flexible as we needed instead today we use. VSLM
VLSM (Variable Length Subnet masks):

This is where we as the Network Administrator can determine what the best subnet mask can be for our particular network. You are able to customize the subnet mask to specific requirements 

Variable Subnet masking allows us to use different subnet masks depending on the requirement. So although a network of 10.0.0.0/8 is a class A network that has that 255.0.0.0 Subnet mask we may want a network with more flexibility So variable subnet mask would allow us to set the Subnet mask to /24 so 10.0.1.0/24 and 10.0.8.0/26 would be VLSM

The real question then becomes what are the size of the subnets, in class based subnetting.

![[Screenshot 2024-07-09 025240.png]]

In variable Length subnet masks the network portion is always gonna be the size of the Network portion of the Class of the ip address it is. For example A class A subnet as above the network will be 8 bits but for a Class B network it would be 16 bits, then the subnetted part is after that. The choice of the network administrator is to determine how many bits in length the subnet is, this comes down to how many host spots are needed in a network.


