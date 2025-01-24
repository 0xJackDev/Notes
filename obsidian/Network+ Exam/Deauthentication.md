
Wireless deauthentication:
- This is a significant wireless DOS attack
- This is where an attacker sends specially crafted frames to disconnect your station from WIFI





802.11 Management frames:
- These are frames that make sure people can connect, disconnect, authenticate or any process involving the network works
- This is important for the operations of 802.11 its how you find access points and connect to WiFi
- Original standard didn't provide any protection for these frames 

This is often used to Deauth someone from the network then when they are reconnecting to the network they reauthenticate and the Four-way handshake is sent over the network and from that the Hashed password is Got and then you can crack and get the Password from the hash


Protecting from deauth attacks
- IEEE has already addresses the problem with 802.11w 
- They encrypted all the deauthentication, dissociate and channel switch announcment frames 
- Not everything is encrypted like beacons, probes, and authentication is not encrypted cause it wouldnt work if it was 
- 802.11w is required for 802.11ac standards