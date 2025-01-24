
VLAN hopping is when attackers somehow find a way to hop from one VLAN to another. 
- This shouldn't happen




There's two primary methods of this
- Switch spoofing 
- double tagging 








Switch spoofing:
- Many switches a network admin will specifically configure an interface on that switch to act like a access port, meaning youll be plugging an laptop or desktop or some other endpoint into it, You can also configure interfaces to be a trunked interface, so that you can send many different VLANs over a single connections in switches, best practice is for the Network admin to manually make these configurations, there are configuration options in the switch to setup an automatic configuration. Meaning when you plug in your device the switch will determine if its an access device or a trunk connection. 
- There's no authentication required, an attacker could plug in with a laptop but tell the laptop to send trunk negotiation down that link to the switch. The switch in the other end will automatically configure it as a trunk connection because it will assume the device is a switch not the Attackers device
- Now you have the Trunk link to a switch and you can send and receive from any configured VLAN because you are the one which separates the VLANs logically
- Switch administrators should disable trunk negotiation/ Auto configuration progess





Double tagging:
When information in a switch is sent across it is tagged with a VLAN header that can be interpreted on the other side. If you add an additional tag on the same frame you may be able to take advantage of double tagging where 
- The first native VLAN tag is remove by the first switch and the second "Fake" tag is now visible to the second switch and forwarded to it 
- This is a one way trip there's no way to get a response back, 
- GOOD FOR DOS
- The way you can prevent this is by preventing anyone from using native VLAN 
- Force tagging of native VLAN 