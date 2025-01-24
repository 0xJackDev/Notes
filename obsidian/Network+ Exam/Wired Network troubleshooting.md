

The longer the distance the more a signal tends to degrade that degrading is called

Attenuation:
- Usually a gradual process signal strength diminishes over distance






we often refer to the measurement of these signals as a decibel
Decibels (dB):
A decibel one-tenth of a bel 
the capital B stands for Alexander Graham bell

This is a logarithmic scale, meaning it varies widely as you stretch it out a longer distance, you are able to Add and subtract losses and gains to find out the signal

3 dBs = 2x the signal 
10 dB = 10x the signal 
20 dB = 100x the signal 

And this scales up more 



dB loss symptoms:
If there's no connectivity or no signal then there will be 0 dB of signal

If the signal is intermittent then you may have some signal getting through but other signal isn't able to be received on the other side. You may have enough signal to sync the link but not enough to transfer any amount of data. 


Poor performance is when the signal is too work, If you see CRC errors that means that the data is being corrupted and you cant transfer data successful 

Its good to get a measurement tool to test each connection





Avoiding EMI and interference

EMI = Electromagnetic interference

First you wanna make sure the cable is not damaged, or twisted too much.


EMI and interference with copper cables
- avoid power cords, fluorescent lights, electrical systems and more.

Test after installation of cables on how much signal you can get





Troubleshooting pin-outs:
- cables can foul up a perfectly good plan, make sure to test your cables prior to implementation




Sometimes the ports on our devices go bad, and you cans tart to see interface errors.
This may indicate a bad cable or hardware problem 




Interface configuration

Auto vs Manual configuration
- this is a personal preference 

If theres no light there's no connection 

The speed on a connection has to be identical on the same side

You will see a link light if there is a mismatch of a duplex, however the speed will suffer later 









Opens and shorts:
sometimes when cables are moved around a lot the internal insulators are moved away and wires start to touch each other, this is referred to as a short circuit. 


A short circuit
- Two connections are touching 
- Wires inside of a cable or Connection


An open circuit
- this is a complete break in the connection 
- Broken wire



in both of these there can be a complete interruption of signals.





If your able to move around the wire someway and make it work then you probably either have a short circuit or your able to somehow get that open circuit connected over a temporary period.


In both of these situations it will usually just be easiest to replace the cable, these things are hard to fix.


If the problem is in the wall or ceiling then you might want yo use a Time Domain Reflectometer (TDR) to see how far exactly down that cable you might have a short/open.








Incorrect transceivers:
If using fiber then you may be using a transceiver in your router or switch to connect that fiber signal to your device. You have to make sure that the transceiver matches the type of fiber. 
- for example single mode transceiver connects to single mode fiber 
- Transceiver needs to match the wavelength being sent over the fiber. So if the fiber signal is 850 Nanometers (nm) then you need to make sure the Transceiver is 850nm 
- Use the correct transceivers and optical fiber, check the entire link
- Its very, very easy to do this because these transceivers look basically the same a lot of the time, so you have to check the wavelength specifications. 







Speed/Duplex mismatch:


If you set your systems for auto configurations you would expect to have them to have the same speed right? Unfortunately Autoconfiguration will sometimes set one end to one speed and another and to another speed 


Same thing can happen with duplex






Another common mistake is reversing the transmit and receive pairs on your RJ45 connection 

- this is very easy to find with a cable tester, it will show you a wire map and its simply to identify



Some network interfaces will automatically correct this this is called (auto-mdix) meaning even though you made a mistake one of your devices is uncrossing this signal and making it work as normal 

the other way to fix this is to locate the reversal location and replace the messed up cable. Its often at a punchdown.





Dirty optical cables:
if using fiber, light needs to be seen and fiber connectors must always be clean

- always use dust caps


- clean before using 