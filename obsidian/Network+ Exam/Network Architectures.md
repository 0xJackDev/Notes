
In this video we will look at a number of of different architectures we use when designing our networks  The first will be a very common one is


the

Three-Tier Architecture:

We will go through what the three tiers consists of, we will start with

The core Tier of the network, this is where we should be running our main applications so for example web servers, databases, and applications. This is the Center of the network and many people will need access to this 

The users though don't connect directly to the core Instead there's a midpoint called the

Distribution Tier, This layer manages the communication between the core and the users not only providing the users with a way to connect to the core but it also provides a way of redundancy and control of traffic into and out of the core, 

and the last tier is the

Access Tier, This is where the users are located and usually there is an access switch somewhere close to where these users are located its common in fact to have multiple access switches on a floor. That floor would roll up to a distribution switch  
![[Screenshot 2024-07-14 224141.png]] This would be the network topology 




SDN (software Defined Networking)

In recent years we have taken the idea of physical networking components and virtualized those systems similar to what we have done with virtual servers. We have been able to take the different functions of these networking devices and separate them into separate plains of Operations in these are

The Data Plane, The Control Plane and the Management Plane All of these together act as SDN

This design fits perfect with our cloud based architectures we are able to take these networking components and break them up into different functional pieces and manage them separately.

For example we may create an Infrastructure layer, Often referred to as the data plane as the part that is doing the real work of the network component for example if it was a switch it may be processing the network frames and packets. If its a firewall or router it could be performing Forwarding, trunking, encryption, Or NAT (network address translation). to be able to forward data to different places is handled by the data plane.


There has to be something to manage what the data plane is doing and that's the job of the control layer often called the Control Plane, 
If your keeping track of where routing tables might be, switching tables, Or Knowing Where NAT is working its all handles by the control layer 
- dynamic Routing Protocol updates



of course we need some way to control all of this as network Admins so we control them through the application layer or the Management Plane this is the application layer and this is where you can control and manage the networking device






Spine and Leaf Architecture:

This is where you have services that connect to leaf switches that connect to leaf switches that connect to spine switches. Each one of these spine switches on the top connect to all of the leaf switches in a network and the leaf switches DO NOT connect to each other they all connect to the spine and the spine determines where the traffic goes from there ![[Screenshot 2024-07-14 225300.png]]

You'll also notice the spine switches don't connect directly to each other all of the communication is either occurring from leaf to spine or spine to leaf.
Its common to associate the spine and leaf architecture with what we call 

Top of rack switching: 
This refers to the physical rack that might be in your data  center You can think of all of these leaf switches as being on the top of a particular 19 inch rack and within the rest of the rack you might have image servers, directory servers, web servers and file servers allowing you to have some very simple cabling between the leaf and the spine 
- fast 
- may be expensive
- simple cabling
- redudant





Traffic flows:
when working in a data centers its useful to know where data is originating and where the destination is. We refer to this path between source and destination in directional terms, for example 


an east-west traffic: 
This is traffic going to devices within the same data center 


North-south traffic:
this is data that is going outside of the data center, since this data is going outside of our network we may have different security postures for North-south traffic then east-west traffic 















![[Screenshot 2024-07-14 225850.png]]