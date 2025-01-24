


Wireless packet analysis:
Wireless networks are very easy to monitor
When your performing packet analysis you may temporarily stop communicating on the network, this is so that you can listen to the other packets on the network, as you cant hear the network if you are transmitting 
- Some network drivers wont be able to capture wireless information and cant be put in listening mode

wireshark.org




Protocol analyzer
this is what Wireshark is 






Speed test sites:
This is useful for bandwidth testing on a device.






iPerf:
This is performance monitoring on your local network 
- need two computers, one as the Iperf server and one as the Iperf client








IP and port scanner

- scan for IP addresses and open ports


Pick a range of IP addresses and see who responds to the scan

- alot of these tools can visually map the network like Zenmap


This is goof for rogue system detection

Nmap/Zenmap, or Angry IP scanner





Netflow:
Gather statistics from all traffic flows,  
- uses probes and collectors to collect data then centralizes it so you can create reports on whats collected 
- The Netflow probe is usually watching network communication through a tap
- The probe then sends the information to a NetFlow Collector which has alot of storage and is gathering stats from a bunch of different Netflow probes
- from this you can make a ARP to view your netflow Collector info 






TFTP server:
Trivial File transfer protocol
- a bare minimum file transfer protocol
- perfect for firmware upgrades  
- Your device acts as the TFTP server and the switch/firewall/router acts as the TFTP client 







