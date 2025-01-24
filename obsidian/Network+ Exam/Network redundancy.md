One way to implement redundant systems is to purchase two devices but have one of those devices operate at any particular time, This is

Active-Passive:
- Two devices are installed and configured but only one operates at a time
- If one device fails the other takes over 
- There's constant communication between the pair to make sure that one is always working at a certain point in time
- Configuration and real-time session information need to be constantly synchronized between both devices





Active-Active:
- You buy two devices and use both at the same time
- More complex to design and operate then Active-passive we have to consider managing data flows and monitoring them. Requires good understanding of system









Diverse Paths:
- This is where you create multiple paths to get from Point A to B
- One way to do this is by using multiple Internet service providers, this way if you lose connectivity to one ISP you can use the backup ISP
- This may require additional hardware and engineering we may have to configure Advanced dynamic routing protocol
- Configure local devices so they understand there is two paths to get to the internet possible
- Great for redundancy






High availability protocols:
- we can also increase redundancy with protocols
- FHRP (First Hop redundancy protocol) your computer is configured with a default single gateway, we need a way to provide availability of the default gateway fails. If using FHRP you can configure multiple routers on your network to work together. If your first hop was to fail the FHRP would allow another router to take over and act as the default gateway
- VRRP (Virtual router redundancy protocol): This is a virtual IP address that is associated with a router and if that router fails the virtual IP address is moved to another working router, allowing you to setup one IP for the gateway and the host who has the IP changes