

Rogue DHCP server:
- there's no inherent security inside of DHCP, an attacker can create their own DHCP server and hand out IP addresses from an attacker,
- If the attacker is using IP addresses that overlap with the existing DHCP server, then there can be invalid or duplicate addresses, which can leave no connectivity
- The way Avoid a rogue DHCP server is to constantly monitor for unauthorized DHCP communication and block that communication
- Enable DHCP snooping on your switch, this will automatically find these rogue servers
- If you are using active directory you can authorize DHCP servers so your active directory knows which DHCP servers are legitimate 
- If you do find a rogue DHCP server you need to disable the interface the rogue DHCP server is on and have all your devices release and renew their IP leases 




Rogue Access point:
This is an unauthorized wireless access point
- may  be added my an employee or an attacker
- Not necessarily malicious
- this is a significant backdoor
- Its very easy to plug in a wireless Access point or to enable wireless sharing in your OS
- Schedule a periodic survey, Use third-party tools like WIFI pineapple, Heat maps 
- Consider using 802.1X, This make sures anyone on the network authenticates properly before allowed access 





Wireless evil twin:
- This is configures an access point to look like an existing network with the intention of getting someone to connect to your access point
- Could overpower the original WiFi 