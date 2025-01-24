
On the internet its estimated there are about 20 Billion devices connection

IPv4 only supported round 4.29 Billion addresses

The address space for Ipv4 is exhausted 

So how are we able to have all of these devices communicating on the internet without enough ip addresses?
we are able to use a technique called Network Address translation or NAT, this isnt the only reason we might use NAT but it is one of the most common reasons.

We are able to use Network address translation to increase the number of available devices because we set aside some very certain IP address ranges as what we call, private IP addresses. This comes from standard (Request for Comments) RFC 1918 , and it spefically assigns what these Private Ip address ranges would be. It is a very big chart. Memorizing the private IP address ranges is the important part. 
a good rule of thumb is if it starts with 192.168 its private
if it stants with 10 its private
if it starts with 172 its private.


![[Screenshot 2024-07-05 224938.png]]



Very simply Network Address Translation is when a device changes an IP address as its communicating through the network. This is commonly done using a router ![[Screenshot 2024-07-05 225135.png]]

On the left side is our private network. And you can see our private address range of 10.10.20.0/24. Meaning our device Vala and our Router are both communicating using this Ip range. But Vala would like to talk to professormesser.com webserver. And you can see that Prof Messer has a public Ip address of 104.20.19.63. We need to find a way for our Private Address to communicate to these Public addresses and back again. 

So we will use our router to perform this translation. Vala Will send an IP packet to the Professor Messer website, which means the source IP is Vala's IP which is 10.10.20.50 and she is sending this message to 104.20.19.63. Once this packet is sent to the Local Router. 
The router recognizes that a private IP address is in use and makes a change to that IP address/ Translates that Ip address to a Public IP that has been previously configured in the router, it then sends the rest of that information to the destination IP. And we can do this because we changed the Source Ip to a public Ip address, this is important when sending data back. 
Obviously we cant send it to the original 10.10.20.50 so the Prof mes website simply sends The response back to the Routers Public Ip address which is 94.1.1.1 so the Destination Ip will be 94.1.1.1 and the Source will be 104.20.19.63. This packet is then sent to router 1 and router 1 has a previous configuration inside of it that says if anything is received on 94.1.1.1 then it needs to be translated to the Internal IP address used by VALA. 


Well that process works fine if there is only a single private ip address, but what if you have multiple IP addresses or Thousands? 

In this situation you will perform a special kind of Network Address translation Called a Source Network Address translation, Or a NAT overload  / Port Address Translation (PAT) 
![[Screenshot 2024-07-05 230008.png]]
Lets take this same situation where Vala needs to communicate to the profmes server. 
When sending the packet from Vala to the router we are sending it from 10.10.20.50 from Port 3233 *Ports are added in Port Address Translation not used in normal NAT* Vala has chosen a random port number as the source port number and Vala is communicating to the destination IP over port 80.

When this info is received by the router the router recognizes that the internal IP address needs to be changed to a Public, but it not only needs to change the Source IP address but also the Source Port number. 
It creates a table inside of the router that translates from the Private Ip address and whats available as a Public Ip address. In this case 94.1.1.1 with a port of 1055 as the public ![[Screenshot 2024-07-05 230301.png]] And now when Professor messer sends its data back itll send the data to the Public Ip address and when the router Gets that packet it will know it has to translate the Destination IP into a Private Ip address so itll look at the table and see what Public address and Port matching the Private Address and port. If you have a router at home or in a buisness its performing this PAT Alot of times a day. 