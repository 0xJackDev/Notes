

Straight through cable:
- Connect MDI to MDI-X
- When connecting ethernet devices we are commonly using what's called a straight-through cable, meaning the wire on pin 1 on one side is connecting to the wire on pin 1 on the other side. Pin 2 to pin 3 and pin 3 to pin3 and so on so fourth. This is sometimes referred to as a Patch Cable, because this is what we use inside of a wiring closet to patch from a patch panel into a ethernet switch 
- this connects workstation to network devices, very common Ethernet cable most eth cables are this![[Screenshot 2024-07-16 035213.png]]
- If you look here on the side where it says transmit is where the data is transmitted but where it says receive data is received this is how data can be sent and received at the same time.
- This traffic flow changes a bit when going into Gigabit ethernet connections that's because on Gig there is both transmit and receive on every pair of wire used![[Screenshot 2024-07-16 035357.png]]





Ethernet Cross over cables:
- connect MDI to MDI 
- Connect MDI -xto MDI-X
if we are connecting two devices together that are both MDI devices for example two separate workstations to each other or connecting two switches together. Instead we would use a crossover cable. Heres how the wires are ![[Screenshot 2024-07-16 035555.png]]


Most ethernet devices can auto detect when a cross over cable is needed and implement what's Known as a auto-mdi-x. Both devices will realize they are the same and internally automatically cross over the communication without needing a physical cross over cable. So this makes it super easy you can just use a straight thru cable and the devices themselves will determine if they will use crossover or not.




If devices are the same devices use Crossover the one exception is if a workstation is going to a router also use a crossover. besides that anything different use a straight through cable.