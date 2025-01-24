DNS stands for Domain Name System its one of the most Popular Protocols on the internet.

It translates human-readable names into IP addressess

DNS is also configured as a Hierarchy

It is also a very distributed database there are many different DNS servers, for example there is 13 root server clusters, which is the primary root servers for everything on the internet. And although this standard provides 13 servers there are actually over 1000 server providing redundancy across the entire internet.


This allows us to half Top level domains or TLDS Either
Generic Top Level Domain (gTLDS) - .com - .org - .net - etc

There are also 275 Country code top level domains (ccTLDs) - .us , -.ca , .uk, etc




DNS Hierarchy ![[Screenshot 2024-07-14 202313.png]]

you could have professormessger.com point to a diff ip address then mail.proffessormesser.com



![[Screenshot 2024-07-14 202413.png]]



Internal DNS
Many times the DNS server we are gonna be using is one that is internal on our own network, we would have it running on our own internal services, our local IT team manages and configures the device It contains DNS info about Internal devices, This DNS service is on a windows server ususally


External DNS:
this is managed by a third party and doesnt have internal device info, Things like google DNS or cloudflare


Behind the scenes of resolving an IP address can take many different forms 

One is a Recursive Process and One is a Iterative Process

Recursive Query:
in this we send our single request to what is usually a Internal DNS server, the Local DNS server then sends out requests to try find the IP address of the Server that we requests, Once that name resolution is completed it then reports back to us on what it found, It is also keeping a very large cache of these requests so if the next person makes this request to this query it will respond back immediately.


Iterative query:
In this you make all the queries ourself directly to these dns servers and theres not central DNS cache pool. Instead the cache is local on our machine.

Basically either do the DNS query yourself or another node does it 


Another important consideration when you are making these DNS queries is the Authority of the response your getting

Non-authoritative:
if you are making a request and the way that is resolves the IP address is through the cache you will see a NON-authoritative answer this means the answer we received didnt come from the Zones source file and is prolly cached information 

Authoritative:
The DNS server is the authority for the Zone 




TTL (time to live):
when info is received on a DNS server that TTL is put next to it in the cache and once the TTL hits zero then the next time we need to find the IP address we will go through the Name resolution process again.
A very long TTL can cause problems if IP changes are made on networks 


Most of the time we are doing Forward lookups to a DNS server meaning we are providing the DNS server with a fully qualified Domain Name (FQDN) and the DNS server responds with the IP address of the domain 


You can also reverse the process where you provide the DNS server with an IP address and the DNS server provides a FQDN this is called a Reverse DNS lookup 


normal dig will perform a forward request 


dig -x *ip address* does a reverse lookup request