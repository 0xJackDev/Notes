
802.11 Technologies:
The frequencies are usually 2.4 GHz or 5 GHz, Sometimes these are used at the same time. 
- Sometimes 802.11 will use both 
- Sometimes they will use additional bands 


Instead of referring to the specific frequencies we tend to refer to these sections of frequencies called 
Channels:
- A channel is a group of frequencies, number by the IEEE 
- Using Non-overlapping channels would be optimal, its best on multiple access points to use frequencies that do not overlap or conflict with each other 

The ranges of frequencies that we are able to use are dependent on the Channel width sometimes referred to as the Bandwidth. 

Bandwidth:
- This is the amount of frequency is use 
- You will commonly see 20 MHz, 40 MHz, 80 MHz and 160 MHz bandwidths

![[Screenshot 2024-07-16 144754.png]]



As you can see using 5 GHz gives you alot more possible frequencies that you could use then 2.4 GHz giving you more room to have more signals that aren't overlapping.

When we increase the bandwidth we are able to use alot more of the frequencies as you can see that is the ![[Screenshot 2024-07-16 144924.png]]
As you can see the Channels cover much more amount of frequencies the larger the Bandwidth is. 






80.11a, 80.11b, and 80.11g use Bandwidths of 20 MHz actually 80.11b uses 22 MHz 



80.11n Has the option to be 20 MHz, 40 MHz, 80 MHz, 
- some of these frequencies are only available inside of 5 GHz like 80MHz doesn't exist on a 2.4 GH network 




80.11ac (20 MHz, 40 MHz, 80 MHz, 80+80 MHz, 160 MHz)
- the 80 + 80 bonds two 80 MHz channels together in two seperate channels. 



80.11ax  (20 MHz, 40 MHz, 80 MHz, 80+80 MHz, 160 MHz):
- same as 802.11ac




when discussing 802.11 standard we will often discuss an Access point or router or some other piece of equipment in the middle of the communication, but 802.11 also supports the ability for stations to talk directly to each other without using any type of access point this is a IBSS

Independent basic service set (IBSS):
- This allows two devices to communicate directly to each other using 802.11 
- This uses Ad-hoc meaning we are creating this connection for a particular purpose and we didn't have to plan out some type of Access point 
- This could be a temporary or a permanent communication






SSID and BSSID:

When connecting to a wireless network there is usually a name in the Operating system, 

SSID (service set Identifier ). That wireless name like for example Bmasion is example of a SSID, this is often referred to as the Wireless network name.



There might be multiple access points supporting an SSID, How does your computer tell them apart. That is with the hardware address of an access point called the BSSID (Basic Service set identifier) 
 - the BSSID is the MAC address of an Access point



Most organizations have more then one Access point, we use the same wireless name across access points in the network which makes it easier to roam from one part of the network to another.

The network name shared accross access point is an ESSID (extended service set Identifer)

If you connect to the ESSID on one end of the building and walk through the building your device will automatically connect to the nearest access points and you don't have to manually reconnect ![[Screenshot 2024-07-16 150459.png]]




Counting antennae's:
![[Screenshot 2024-07-16 150743.png]]




Before MIMO data was sent as a straight stream across the network. 

After mimo, alot of different data packets were sent at once through the multiple antennas and the waves would bounce off other computers and the be received by the receiving antenna. the data would then be reconstructed through advanced digital signal processing. 

When introducing MIMO we were able to send alot more traffic at once and multiple streams of traffic at once. With each Upgrade of MIMO the the amount of more data we could send is just more.

When we introduced MU-MIMO we could now send multiple users Multiple streams of data at once. Instead of just one computer multiple streams of data at once. 


To more intelligently send data we can use 802.11ax MU-MIMO with Orthogonal Frequency division Multiple access (OFDMA) which makes it so we can send multiple streams of data and break those streams into smaller pieces of data and breakup data as needed. Meaning the end stations can get EXACTLY the right amount of data and we can use our wireless network most efficiently.




Omnidirectional antennas:
- the most common type of antenna
- signal is evenly disturbed on all sides
- good choice for most environments 



Directional Antennas:
- this allows you to focus the signal 
- Can reach farther distances
- Antenna performance is measured in decibels or dB 

Yagi antennas is very directional and high gain antenna

a parabolic antenna focuses the signal to a single point 