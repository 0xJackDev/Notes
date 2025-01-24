
Fault Tolerance:
- we need to maintain uptime in case of failure
- Fault tolerance adds complexity 
- RAID, Redundant power supply's, and redundant NICs are examples, so is a load balancer 







Redundancy and fault tolerance:
- redundant hardware components in case one part fails you have a backup part 
- RAID ( Redundant array of independent disks)




High availability: (HA) 
- this is that the server is always on and always available 
- Problems should automatically identify and fix themselves with HA
- May include many different components working together 







NIC teaming:

Load Balancing / Fail Over (LBFO) 
- this allows you to have multiple links between devices so incase you lose one link you still have another
- this is useful for redundancy 
- Usually integrated by having multiple Network interface cards in a device hence NIC teaming 
- NICs talk to each other if they stop talking youll  know it goes if and youll know not to use it
- This can double bandwidth though since you have double the links