

If you have to configure a DHCP server we have to put all the Configuration settings into the server in order to provide this info to ur clients you need to create a 


DHCP Scope:

The scoppe includes many Properties but One of the most important ones is the IP address range, And the Subnet mask, And how long a DHCP lease is, You may also want to add any other important info like, VOIP servers, Default gateway, or DNS servers


This grouping of IP addresses is called a POOL and when a client needs an IP address, It sends a request to the DHCP server and the DHCP server assigns a IP address from any IP address available in the POOL, 

A DHCP server could also have a scope of addresses, the scope is a single continuous pool of IP addresses, You can make exceptions in this cope of IP addresses not to assign to clients 




Many DHCP servers are configured with a dynamic assignment, 
this means theres a large pool of IP addresses and when a node needs an IP address it pulls one from the pool after the lease period is expired if the device does not renew the lease then the IP address is added back to the available pool,
Many DHCP servers have an Automatic assignment process meaning once an IP address is assigned to a computer that IP address will always be available if possible meaning if you leave for a week and come back you should get the same IP address over and over again 



Instead of randomly assigning an IP address from a pool, We can also configure our DHCP server to assign a static IP address this is especially useful if you have a server and you want that server to have the same IP address every time,
To do this you would go into the DHCP configuration and Add the Mac Address a Matching IP address, so every time that someone makes a request for an IP address the MAC address is identified and the matching IP address assigned, 
This is referred to as Static DHCP assignment, Static DHCP, Address reservation and IP reservation


Alot of SOHO Routers have this (Small office/Homeoffice) and you can configure the DHCP server in LAN setup, 




DHCP leases:
![[Screenshot 2024-07-14 200234.png]]



There are two important timers to know about during the DHCP process, the first is the T1 Timer
this is the timer that the client uses to check back in with the lending DHCP server to auto renew the IP address, By default this is 50% of the lease time.

Theres a second timer called:
T2 Timer:
if the original DHCP server is down or unavailable the T2 server will bind with any available DHCP server 87.5% of lease time 