


Cable crimpers:
This will allow you to fasten an RJ45 connector onto the end of an ethernet cable





![[Screenshot 2024-07-20 225148.png]]![[Screenshot 2024-07-20 225234.png]]



Get a good crimper 

Practice takes perfect.






Punch down-tools:

This allows you to Punch a wire into a wiring block

This can be tedious as every wire must be individually punched








Tone generator:
Puts an analog sound on the wire, 

Then we use an inductive probe on the other end so that we can find the wire on the other end, and it doesnt need to touch the wire either.


- this can save hours of time with easy wire tracing. 








loopback plug:
- this is useful for testing physical ports 


takes signal coming into the loopback plug and puts it right back into the device its being sent, this can be seen over serial connections, Or Network connection like Ethernet.

These are not cross-over cables


If you send data to a loopback plug and compare the data that you sent from what you received back and its the same the device is prolly working right if its corrupted youll see there's an issue 





TDR and 
Time Domain Reflectometer (used for copper) / Optical Time Domain reflectometer (used for fiber)
- these devices can estimate cable length
- Identify splice location
- Check the signal losses
- and certify that a cable installation was down properly. 



The TDR works by sending an electrical pulse down the cable and then listens if anything is reflected back to the TDR, if there's a problem with the cable, a break in the wire or any different in impedance of that copper a reflection will be sent back to the TDR, the TDR will then calculate different things like time and distance
OTDR does the same thing with light



- These tools can be expensive, especially a OTDR 

- requires additional training


- very powerful 






Multimeters:
- one common use for a multimeter is to provide AC voltage measurements to check wall outlet voltage.
- You can also check DC voltage, for example the CMOS battery power
- You can also test for Continuity, you can use one probe on one side of the wire and one on the other side of the wire and if it beeps then there's continuity across the wire 










Cable testers:
- you simply plug the two sides of the cable tester into a wire and it will very quickly show you what the wire map might be 
- Can identify missing pins or crossed wires.
- Not useful for frequency testing








Taps and port mirrors:
- Intercept network traffic and send a copy to a packet capture device 



- physical taps
	- this is where you physically disconnect the link and put a tap in the middle if the physical tap doesn't require any additonal power then you are using a passive tap if it requires power its a active tap 



Port mirror
- You have a port mirroring capability build into your switch, in cisco it is called a SPAN, 
- This allows for a software-based tap 
- Limited functionality but can work well in a pinch





Fusion Splicer:
This joins two ends of fiber together, 
- you can add a connector to end of fiber
- Extend length of fiber
- Or remove a section of fiber
- Fusion splices use heat to connect the fiber together
- Requires training to use 
- This is expensive af


Light meter:
- This allows you to see how much light it being received through the other end 
- you would send a light through one side and measure on the other end





Spectrum analyzer:
Managing wireless access points can be a challenge we have to make sure our Signals aren't overlapping

A spectrum anaylyzer allows you to see all that's communicating on the frequencies near your area 