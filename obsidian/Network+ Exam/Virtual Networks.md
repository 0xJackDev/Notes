
The way we manage data has changed rapidly over the last few years. and the way we deploy networks has changed too. we used to have server farms with 100 individual computers inside and servers inside of them. Lets say we have a server farm with over 100 individual computers all working together on a network. This enterprise network is usually connecting all of these devices using multiple VLANS, Redundant connections, and high-speed communication. But with virtual servers, we've realized we don't need 100 different physical servers, instead we can create 100 virtual servers that may be located on a single physical device. So this brings us the question if we are collapsing all of these servers into one single physical device, what happens to our network? 



Network Function virtualization (NFV)
If we are replacing physical servers with virtual servers then we are taking all of our physical network and replacing it with a virtual network. This is called NFV where we take all of our network devices and the entire network infrastructure and move it directly into the hypervisor. This means all of our switching, all of our routing, load balancing, firewalls, etc is all now contained within this virtual system. This provides us with the same functionality as a physical device, but in many cases provides us with additional capabilities for example when you need a new switch or a new router  you dont have to go purchase a new router you can quickly and easily deploy network functions from the click of a few buttons.



The hypervisor
This is the virtual machine manager or VNM. this is responsible for running all of our virtualized instanced and the virtual network connections. the hypervisor is responsible for managing access to  the Hardware from the hypervisor but it can all be managed from the central console.




vSwitch
Virtual switch 
now that we know all of our virtual machines are located in and managed by the hypervisor now we need to have a network that connects all of those virtual machines. We connect this through a vSwitch in a vSwitch we are simply taking the physical switch that we used to have and moved it to the virtual world. We can still do all of the things that a physical switch can do like Port mirroring, link aggregation, set forwarding options, NetFlow, etc. Deploying one of these vSwitches is easy from the hypervisor this can also be automated by the hypervisors API.



Virtual Network Interface Card (vNIC)
Every machine needs a network interface so they connect to the network. this includes virtual machines, Virtual machines use a Virtual Network interface card in order to connect to the rest of the network. This is also usually configured throughout the hypervisor. You might wanna have multiple vNICS so that you can have additional features. 