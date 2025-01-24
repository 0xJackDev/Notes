

PING 
- test reachability to a IP address 
- one of your primary troubleshooting tools to see if you can reach a host
- the TTL refers to the number of hops the packet took





ipconfig / ifconfig / ip addr
- This allows you to view TCP/IP network adapter information





nslookup and dig:
- looks up information from DNS servers

nslookup 
- looks up ip address


dig (domain information groper) 
- not included in windows but you can get it
- Views DNS info



traceroute:
- tracert in windows traceroute in Linux
- this creates a route that a packet takes through all router between point A and point B and figures out what exactly hops a packet goes through
- Takes advantage of ICMP time to live excedded messages, for example TTL=1 is the first router TTL=2 is the second ETC.
- Not all devices will reply with ICMP time exceeded messages these are firewalled out or prevented 



Flavors of traceroute:

Traceroute doesnt work the same in all Operating systems for example windows sends a ICMP eco request 

- other operating systems like Linux allow you to specify the protocol used






Address resolution protocol:

- Determine  a MAC address based on a IP address 

arp -a will allow you to view the ARP cache on your local machine 







netstat:
- stands for network statistics 


- netstat -a shows all active connections

if you would like to see the executables that are creating this traffic in windows you can use 

netstat -b 


and if you only wanna see IP addressed and not domain names use 

netstat -n 






hostname
:This allows you to see the fully qualified domain name and IP address of the device 




Sometimes its useful to see a devices routing table 

on windows you can type route print 

and on linux you can type netstat -r 





Telnet:
- this has more functionality then most think 
- telnet can be great for checking if a port is open for example -telnet 10.1.10.1 443 would check if any traffic is running on 10.1.10.1 port 443 





nmap: 
Network mapper 