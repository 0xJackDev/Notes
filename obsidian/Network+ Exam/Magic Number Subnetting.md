
![[Screenshot 2024-07-10 144352.png]]

11111111.11111111.11111111.11000000

11000000.10101000.00000001.00000000



Total Subnets = 2 bits = *amount of subnets*^2 = 4


Host per subnet = *Amount of Host Bits* = 2^*hostbits* - 2 



Ultimately we are looking for four important addresses The network address, The broadcast Address, The First Avaible and Last avaible Host addresses. In order to convert this to binary we would have to do all of the conversions for that network address and subnet mask to be able to determine what all of these things are. This takes a Pretty long time. 


One popular shortcut thats used for this subnetting process is called the magic number method, this requires Minimal Math 

Some charts might Help you like for example a CIDR to Decimal chart, One of the things you will notice is there is some repeating values involved in calculating these. 


![[Screenshot 2024-07-10 145741.png]]

Now that we found the Intresting Octet we need to perform a calculation The calculation will be 

256 - *intresting octet* =

so in our case 256 - 240 = 16 

We call this 16 number the Magic number, This is the number of hosts that is on that subnet![[Screenshot 2024-07-10 145942.png]]

We see our Ip address is a 77 Which is between 64 and 80 this means that our Subnet ID in this particular example is 64 So we can Have a Subnet id of 165.245.64.0 

Now that we know our Subnet ID we have to find the Broadcast addr 
so we follow the same rules If any mask is 255 copy the IP address if the mask is zero bring down a zero. and find the interesting octet

This follows the EXACT same process as the Subnet ID Except replacing the IP address part with the Subnet ID part c
265 - *interesting  octet* = 16

In this case we are gonna calculate a broadcast addr and the way we do that is using the Magic Number and by taking the Subnet ID, Adding the Magic number to that then subtracting 1 will equal our Missing Octets value so in this case


64 + 16 - 1 = 79 
So the Broadcast addr is =
165.245.79.255

Network ID/Subnet ID = 
165.245.64.0 

Find the Host range

Host range = 
Subnet Id + 1 = 
165.245.64.1 



Last Host = 
Broadcast address - 1 
165.245.79.254


Now we have all we need to perform calculation

256 - 248 = 8 

Ip address is 180 so refering to the chart the number right under 180 is 176

10.176.0.0

10.0.0.0


If there is a 0 in the Subnet mask when looking for the Broadcast address make sure you bring down 255 because its supposed to be the last usable addr 

we use the magic number

We need to calculate the Broadcast Address by taking the Subnet ID + magic Number - 1 

10.183.255.255![[Screenshot 2024-07-10 151315.png]]



Subnet ID:
10.176.0.0

Broadcast addr:
10.183.255.255

First Host:
10.176.0.1

Last Host:
10.183.255.254