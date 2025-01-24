
When we communicate online we usually assume the two devices that are talking are the only devices involved in the conversion. Attackers realized if they can get in the middle of this information they can see/modify info as its going across the network, Used to be referred to as a Man in the middle attack but is now a On-path attack 
- Works by having a attacker intercept your traffic then redirect it.





On a local subnet one simple way to have an on-path attack is with 
- Arp (address resolution protocol) Poisoning 
- Since ARP has no security we can manipulate the ARP cache so when someone tries to send an packet to say the Routers IP address it looks at the ARP cache and sees the the IP matches with a MAC address and sends the data to the MAC address, ARP spoofing allows you to make that IP address associated to your MAC address instead of the routers.![[Screenshot 2024-07-19 004239.png]]






DNS poisoning:
- This would allow you to perform an on path attack to people not on your network
- Modify the Entries inside the DNS server to route to your servers IP address
- If you are trying to change where one device is communicating you can modify the DNS hosts file as the Host file takes precedent over DNS queries 
- You could also just send a fake response to a valid DNS request 


Theres many other on path attacks 

Like HTTPS spoofing, Session hijacking and Wi-FI eavesdropping
- Encryption fixes most of these sitatuons