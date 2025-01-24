DNS records:

if you were too look at the configuration of a DNS server you would see a number of different records that have been defined in that DNS database. 
We refer to these as 
Resource Records or (RR) and there are many different RR's theres over 30 different Record types.

We will look at the most popular ones.


This is what a very basic configuration inside A DNS server will look like, 

We refer to this as a sample forward lookup file, inside of this configuration file ![[Screenshot 2024-07-14 205900.png]]



Inside of this config file we will be able to see information about the domain in general and more specific records in the domain




At the very top of the configuration is the 

Start of Authority (SOA) record this is the part that describes what the DNS server is managing, It describes the DNS zone details,  The structure of the Domain including the names of the zone, serial numbers associated with the configuration, refresh/retry and expriy timeframes and caching information and TTL information


Most of the time we are making a request to a DNS server that contains a fully qualified domain name and we are able to receive an IP address in return. The way we are able to recieve this IP is because inside the DNS server is an address record


This Address record is sometimes referred to as an (A) record for Ipv4 or (AAAA) for Ipv6
If you ever have to modify the IP or name of a device then your probaly gonna modify one of these A records 



There may be times where we have one IP address thats handling many different services for example you might have a server handling ftp services, mail services and www services all on the same IP address and instead of putting different Address (A) records we will put 

Canonical Name records or  (CNAME) Records, these are records that provide analias to an already existing server.




There may be times when you wanna use DNS to help clients on your network find another service and in those cases we will want to create a 

Service Record Or (SRV) record:
IF your network has a Windows domain controller, Instant Messaging sever, Or Voip gateway. Then we want might to create a service record that identifies where that particular device might be.
For example on this particular network there is an LDAP server and that LDAP server is located at s1.domain.com 


Almost all the domains you work with are going to use some type of email service and if there is then you will need a

Mail Exchanger Record or (MX) record: 
This record contains the name of the mail server which you could then perform additional queries on what the IP address could be, But the Mail exchanger record is relatively straightforward.





Name Server Records or (NS) records:
In a previous video DNS was described as hierarchy of name servers for this to work we need to have references in our name server that will point to other name servers, so we will need to add a record called a Name Server Record. and if someone is trying to find a Name server for your domain that can simply query a NS record.



Pointer Record (PTR) record:
Earlier we saw we could look at address records and query a DNS server with a FQDN and receive back an IP address because we have an address record. We can create the reverse of a Address record and that's called a pointer record so when dig -x ** this how a reverse Dns lookup looks.




Text Records or (TXT) record:
There may be times when we are not adding a DNS name or IP address but instead we put some type of txt into our DNS server this Might be something like a 
SPF Protocol Record (Sender Policy Framework) record, this prevents someone from spoofing email from our domain the SPF record allows mail servers to check if the email did really come from our domain, 

Another type of text record might be a 
DKIM (Domain Keys Identified Mail) record, this allows us to digitally sign our mail and we can put the Public key in the DKIN record so it can be verified by the receiver to lower chances of being stopped by spam filters 




Zone Transfers:
These DNS servers are very critical to maintaining uptime and availability of your services so we need some way to provide Redundancy of DNS services. We do this by using 
Zone transfers, Zone transfers allow us to make DNS changes on a primary DNS server and allow all of those changes to be replicated to a secondary DNS server This ensures any changes we make synchronize to a secondary server.
Going back to the Start of Authority Record there is an entry for a Serial number that serial number specifies the version number of the DNS entry's if we update the serial number your DNS server will recognize there's a new version of the configuration and a Zone transfer will occur,
Although useful we need to make sure not anyone can just initate one of these zone transfers as 


Full zone transfers can be a security risk as Attackers can use the data as reconnaissance for example they could perform a Zone transfer and forward it to their own local machine and get all of your internal names and IP address for ALL records and get all DNS records 