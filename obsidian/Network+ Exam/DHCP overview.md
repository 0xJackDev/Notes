
In the early days of TCP/IP everything you had to setup manually all IP addressing and Subnet masks and gateways and DNS servers, NTP servers etc would have to be configured 


in 1997 DHCP or Dynamic Host configuration protocol was released 


Managine DHCP in the enterprise 
Since DHCP messages are sent as a broadcast and broadcast doesn't go over routers this is annoying cuz you don't wanna put individual DHCP servers on each subnet What you wanna do is have multiple servers for redundancy 

To be able to do this we use what's called a DHCP relay or a IP helper function to rely the broadcast to a local DHCP server