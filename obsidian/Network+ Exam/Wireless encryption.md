
If using a wireless network then you are probably sending sensitive info over this network. We need to limit access to this data to secure all of our data.


We also need to authenticate users before granting access to the wireless network. This often requires a Username and password, and often there is even multifactor authentication involved.

This ensures that all communication is confidential. we also have to encrypt the wireless data. 

We also need to verify the integrity of all communication, we need to make sure the received data should be identical to the original data sent 
- we do this with a message integrity check (MIC) to

We need to ensure Authentication, Confidentiality and Integrity 



WPA (Wi-Fi Protected Access):
This is one type of encryption you might see on a legacy Wireless network
- This was the original version of WPA 
- introduced in 2002
- This was a replacement for WEP (wireless equivalent privacy) WEP SUCKS you can literally just brute force the 6000 possible codes. NEVER USE WEP 
- We created WPA using the encryption cipher of RC4 along with TKIP (Temporal Key Integrity Protocol). This includes a larger Initialization Vector and they encrypted the hash being communicated across the network 
- Every packet gets a unique 128-bit encryption key





Wireless encryption:
- the problem with wireless communication is it is data being sent over the air. If you have the proper equipment and know the frequency anyone can listen in to the information from the air and look at it. 
- The solution to this is to encrypt all the data over the wireless network
- commonly done using WPA2 and WPA3 






WPA2 and CCMP:
Wi-Fi protected Access 2 (WPA2)
This was made in 2004 
- This uses a block bode of encryption called CCMP, CCMP stands for Counter mode with cipher block chaining, Message authentication code protocol. Also referred to as Counter/CBC-MAC protocol 
- CCMP Block Cipher mode
- This isnt just one technology Its a combination of technologies 
- CCMP uses AES (American encryption standard) encryption 
- It uses CBC-Mac for the Message Integrity Check (MIC) 






WPA3 and GCMP 
Wi-Fi Protected Access 3 (WPA) 
- GCMP Block Cipher mode 
- Galois/Counter Mode protocol, this is a stronger encryption than CCMP and WPA 
- GCMP still encrypts data using AES 
- Performs Message Integrity Check (MIC) with Galois Message authentication code (GMAC)







The WPA2 PSK problem:
- today there's not many signific vulnerabilities with WPA2, but there are some shortcomings with WPA2 that could allow someone to perform a Brute force attack on a captured Hashed-password.
- There is a handshake that occurs called a four-way handshake between the client and the Access point when connecting to a WPA2 network. If using a pre-shared key or password there are ways to Capture the Password hash sent accross the network. 
- With the hash itself its basically useless unless you can someone crack the hash with a wordlist :3 
- Tools like airmon-ng make this rlly easy to capture the hash then just use hashcat to break it :3. If you want run it through bluecode hash finder to see if the hash has been cracked before 
- With the hash attacker can brute force the Pre-shared key (PSK)
- If you are using a common PSK or one thats already been breached. 
- Make sure you use a very unique complex password 





SAE:
WPA3 changes the PSK authentication process, 
- this uses something called mutual authentication, where you are not only authenticating to the Access point but the Access point is authenticating to you. 
- With WPA3 Both devices create a shared session key without sending that key across the network 
- No more Four way handshake, No more brute force attack since the shared session key isn't sent across the network 
- Adds perfect forward secrecy, Even if the key was somehow acquired by the hacker they still couldn't get to the information in the wireless communication because each communication is using its own separate session key 
- This method of creating a shared session key without sharing across the network is called Simultaneous Authentication of Equals (SAE) 
- This is a Diffie-Hellman Derived Key exchange with an authentication concept, very similar
- Every user is gonna have a different session key even if they all are using the same PSK 
- this is built into the IEE standard, referred to as the dragonfly handshake 






If you go to your access point you can configure the access point with the Right security levels. 


- In our homes we commonly use a shared Pre-shared key. This is usually called Wpa-2/3 Personal or WPA2/3-PSK method
- On a enterprise or corporate network we don't wanna use pre-shared keys instead we would use individual usernames and passwords for each users. This is probably gonna be called WPA2/3 Enterprise or WPA2/3-802.1X. This Authenticates Users individually with an authentication server (i.e Kerberos or Radius or Active Directory)