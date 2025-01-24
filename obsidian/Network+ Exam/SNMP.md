- Simple Network Management Protocol


- SNMP consists of a centralized database of information contained within our information databases we refer to this database as the MIB or the Management information base. 
- Inside of the Database are a series of statistics we can gather from these devices, we call these Object identifiers or OIDs 
- Poll Devices over UDP/161 
- SNMP v1 - The original , this has structured tables, 0 Encryption over the network, Not used often
- SNMP v2 - This is a good step ahead, With data type enhancements, Still 0 encryption so not used often
- SNMP v3 - This is the new standard, Extensive Encryption and message integrity and authentication




To be able to receive information from these devices we need to know what to be able to ask for. and the information we are asking for is called a 

SNMP OID (object identifier):
This is the information we are asking for, these OIDs are series of numbers for example .1.3.6.1.2.1.11.29.0, each one of these numbers is refering to a different part of the SNMP tree. The first number 1, refers to iso(1), the second number stand for org(3), the third for dod(6), the fo urth for internet(1) and so on. so you could spell out what each one of these sections by their number but when requesting for this info all your sending out is a series of numbers 
- Every variable in the MIB has a corresponding OID
- Some are common accross devices
- Some manufactures define their own object identifiers 
- THE SNMP manager requests information based on the OID 
- With the right type of software you can query a MIB and find all the OIDs on a IP address 








SNMP traps:
As far as we has described is the SNMP process as proactive where we have to query the device. 
This means each device needs to be constantly checked and polled in order to see if its working properly with hundreds of devices this becomes increasingly difficult 
- Instead we can configure the remote device to be able to perform its own monitoring and when it outreaches a certain value it will send a message to us, instead of us constantly having to perform monitoring
- It sends this alert over UDP port 162
- Allows us to be alerted immediately  if a problem occurs if we have configured it correctly 