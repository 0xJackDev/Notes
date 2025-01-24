


Hub:
This is a basic form of ethernet connectivity. 
- Referred to as a Multi-port repeater
- Traffic going in one port is repeated to every other port
- OSI layer 1 
- If you are using a hub everything is half-duplex meaning you can either send information to the hub or receive information from the hub, but you cannot do both at the same time
- This becomes less efficient as network traffic increases
- most hubs have 10 megabit / 100 megabit Speeds
- Difficult to find today











Bridge:
Before the advent of switches we were still able to separate networks and send traffic between those networks between destination MAC address using a technology called a bridge
You can think of this as a switch that has a limited number of ports on it usually two or four 
- OSI layer 2 device as it distributes based on MAC addresses like a switch 
- Connects different physical networks 
- can connect different network topologies together
- A wireless access point is a modern bridge between a wired ethernet connection to a wireless connection





Switch:
This is another modern type of bridge.
This basically does the same function as a bridge because its making forwarding decisions based on the destination MAC address of the data. The different between typical software-based bridge and todays modern switches is that Switches today are able to use hardware to make these decisions More specifically
ASIC or 
- Application-specific integrated circuit (ASIC) 
- OSI layer 2 device 
- Many ports and features, These could possibly provide power over ethernet (PoE)
- Switches alot of times are the core of an enterprise network 
- Some manufactures Added Routing capabilities built into switches these are called multilayer switches or Layer 3 switches 










Router:
- Routes traffic between IP subnets
- OSI layer 3 device 
Its often to use a router to connect diverse network types so for example connecting a Local Area network to a Wide area Network or A copper connection to a fiber connection 









Access point:
- Not a wireless router a wireless router is a router and an Access point in a single device
- This access point acts as a bridge, extending the wired network onto the wireless network
- OSI layer 2 device 
- These just extend the wireless connection so that you can send radio waves closer and have one closer to you to communicate with your network so you can have wifi cover everywhere







Cable Modem:
If you are using a cable company then you probably have a cable modem this is connecting to a broadband network meaning you are transmitting stuff across this network across multiple frequencies meaning you can have many different traffic types or even television types using different frequencies on the same cable .

The data frequencies on the cable are separated Out by the cable modem in a standard called 
- DOCSIS (data over cable service interface specifcation)
- this supports a wide range of speeds 
- high speed networking supported 





DSL Modem
ADSL (Asymmetric Digital Subscriber Line) If you are not using cable for your internet connection you might be using a DSL modem.
ADSL uses telephone lines to provide this internet connection using a DSL modem 
If it is Asymmetric DSL that means the Download speed is faster then the upload speed 





Repeater:
If you want to extend a network connection beyond a typical range you might want to use a Repeater 
A repeater receives a signal, Regenerates that signals and sends that signal out on another interface 



![[Screenshot 2024-07-15 013102.png]]










Converting media:
OSI layer 1 
- Physical layer signal conversion
- to extend a copper wire over a long distance use a media converter to convert it to fiber send it far then convert back to copper when at the destination