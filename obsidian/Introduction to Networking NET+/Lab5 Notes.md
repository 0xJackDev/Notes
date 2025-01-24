
Dynamic Host Configuration Protocol (DHCP) – a protocol that allows devices to automatically obtain network settings (such as IP address, default gateway, etc.) so they can communicate on the network. DHCP uses UDP ports 67 (Server) and 68 (Client)

Reservation – with DHCP, the process where an administrator assigns an address for DHCP to give to a client

Media Access Control (MAC) address – the physical address burned into the ROM of an Ethernet network card; used by switches at the Data Link layer of the OSI model to move information between nodes on the same network

Domain Name System (DNS) – the protocol used to map hostnames and domain names to an IP address on the Internet. DNS uses UDP port 53 for initiating requests

Fully Qualified Domain Name (FQDN) – the domain name that specifies the exact location of the specified node in the DNS hierarchy

Forward Lookup Zone – the zone used by DNS clients to obtain information such as IP addresses that correspond to DNS domain names or services in the zone

Host (A) record – the DNS record that links a FQDN to an IPv4 address

Host (AAAA) record – the DNS record that links a FQDN to an IPv6 address

Alias – a secondary name assigned to a host within DNS – allows an administrator to provide multiple names the same host can respond to

Reverse Lookup Zone – the zone that provides mapping from IP addresses back to DNS domain names

in-addr.arpa – The reverse lookup zone used by IPv4 to map IP addresses to DNS names


Pointer (PTR) record – the DNS record that links an IP address to a FQDN – used for reverse lookups




The Address Pool shows which addresses are available for DHCP to distribute to a scope as well as any configured exclusions.  
The Address Leases shows all addresses that have been assigned by the DHCP server to clients. At this time, there will be no items to show in this view, as the scope has not been activated.
 The Reservations shows any addresses that an administrator has manually configured for a DHCP server to assign to a client. Creating a DHCP reservation ensures that the DHCP client always receives the same IP address even though it has been configured to automatically obtain its IP address via DHCP. Note that no reservations exist at this time, but information is displayed on how to create one. 
 The Scope Options shows all DHCP options that have been configured for just this scope. Windows DHCP server will also list any server options that have been configured in this list as well, but will not allow an administrator to modify them from this screen. Since the Router option was configured via the wizard, it appears in this list.