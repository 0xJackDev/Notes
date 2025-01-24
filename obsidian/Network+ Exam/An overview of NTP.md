If you look at all of the devices on your network all routers, switches, workstations etc have a clock where you can see the date and time on device. And on most networks keeping a synchronized clock is critical for log files, Authentication information and outage details


Network admins get to determine how often Updates to how clocks work

NTP is very very accurate and accuracy is better then 1 millisecond on a local network 


On your Network theres gonna be NTp servers and NTP clients 


NTP servers:
- Listens On UDP port 123 and responds to time requests from NTP clients 
- Does not Modify their own time



NTP Client:
- Request Time updates from NTP server 



NTP client/server
- this is if a device is both a NTP server and client so its just Acting as both a client and a server




Its important to plan your NTP strategy to know what devices will be NTP clients or servers or both





NTP stratum layers:
When making changes to your local network its important to know how accurate that date and time might be. We refer to the accuracy of an NTP as a Stratum value.

For example a
Stratum 0 is effectively an atomic clock providing the exact date and time this is something you might get from something like GPS systems or US naval Observatory has a Atomic clock.

Stratum 1 
This is Synchronized to Stratum 0 servers and this is what most time servers on your network will be 


Stratum 2 
this is when your synchronizing from a Stratum 1 network. 

As you keep going like a Stratum 3 would be when synchronizing from Stratum 2 and so on so fourth



