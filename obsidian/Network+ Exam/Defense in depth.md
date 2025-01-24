
There's no security technique that is 100 percent gonna keep attackers out, instead you wanna layer your defense techniques across a broad array of different technologies for example you might start with

- Physical controls 
	- Door Locks, Fences, Rack Locks, Cable wires, Cameras, etc


Of course we also have to protect against people coming in through the network so we might include
- Technical Controls
	- This is hardware and software designed to keep things secure
	- Things like Active directory, Firewalls, Authentication and disk encryption are examples

Of courser we need policies and procedures for stuff like onboarding and offboarding of employees for this we have
- Administrative controls
	- Polices and procedures









Defense in depth
- Firewall
- Screened Subnet /DMZ zone
- Hashing and salting passwords
- Authentication for network 
- Intrusion Prevention system







Physical segmentation:
- This is separating devices, Creating two separate physical networks Because theres a physical disconnect between the two networks theres no way for these two networks to talk  



Instead of a physical segmentation you can use
- Logical segmentation with VLANs on switches
- You cannot communicate between VLANs without a layer 3 device







Screened subnet:
- Previously known as the demilitarized zone (DMZ) 
- This is an additional layer of security between the internet and you with public access to public resources 

![[Screenshot 2024-07-18 020117.png]]




Separation of duties
- Split Knowledge:
	- Not one person knows all of the details
	- For example half of a safe combination 
- Dual Control:
	- Two people must be present to perform the business function
		- Two keys to open a safe 






Network Access Control (NAC):
If you have ever logged into a network at work, you've probably noticed you use your own username and password that's unique to you.  In a corporate environment we dont use PSKs. Instead we implement.
IEEE 802.1X - Port-Based Network Access Control (NAC):
- When we refer to port based Network Access Control we are talking about physical interfaces on a switch not TCP or UDP ports. This method prevents anyone from communicating on this switch until they have performed the correct authentication 
- Makes Extendible use of EAP and or RADIUS
	- (Extensible Authentication Protocol) EAP
	- (Remote Authentication Dial in User Service) RADIUS
	- EAP is the remote backend protocol used for authentication, while RADIUS is the remote Backend database that is used for authentication with EAP, but we could use any type of authentication protocols and different types of authentication databases. For example we could use LDAP with active directory
	- 
![[Screenshot 2024-07-18 020822.png]]
![[Screenshot 2024-07-18 021121.png]]