
As a network admin you will be asked to connect many kinds of storage systems to your network One of these might be a 


Storage Area Network (SAN):
This Looks and feels like a local storage device
- block level access allowing for Writing over small "blocks" of a file
- very efficient reading and writing
- Requires alot of Bandwidth




Another common High speed storage method is

Fibre Channel (FC):
This allows you to connect servers and storage together in a very high speed network 
- 2, 4, 8, and 16 gigabit per second rates supported
- Supported over both Fiber and Copper
In order to use Fibre channel you will need a Fibre channel Switch you would usually connect your servers (fibre channel refers to them as the iniators) to plug into the fibre channel interface on the switch. You will then connect to the storage system called the target using some form of connectivity like eSATA for example commonly though SCSI, SAS, or SATA


Fibre Channel Over Ethernet (FCoE):
Of course not all servers have Fibre channel interfaces so you can use FCoE with no extra hardware needed but you are gonna need to integrate with a existing Fibre channel infrastructure, Not routable info







iSCSI:
Internet Small computer systems interface 
This allows you to send SCSI commands over an IP network 
This makes a remote disk look and operate like a local disk