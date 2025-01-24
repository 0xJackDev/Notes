

traffic logs:
if working with switches, routers or firewalls etc there's probably logs in that device that help you identify traffic flows 
- these can be very detailed and show every flow from every device 
- This is important for historical information and for monitoring and post event analysis 






Audit logs:
different devices and protocols are gonna have different logs for example if you have Microsoft active directory its gonna have  a series of audit logs that allow you to see who logged in and out of the network. 
- Allows us to keep historical view of network logins 





Syslogs:
When looking at logs youll see that each one of those logs types are very different but they all contain information that can correlate to each other, Although all logs contain very different information we can use a standardized process to retrieve those log files from  every single one of these systems using a standardized protocol called syslog. We can configure all these devices to send info to a consolidated logging receiver which is usually a SIEM or (Security information event manager) 






Severity Levels:
- Not all alerts have the same priority 
- Low level bugs or high level critical alert
- We can use these alerts as a filter and only show Warning level and higher or critical or higher
- You get to decide the importance of each alert level




Interface errors:

Runts:
- these are frames that are less then 64 bytes, the min size of a ethernet frame is 64 bytes so if you receive a frame smaller then 64 bytes that usually means a collision has occurred.
- Most networks are full duplex so identifying a runt is important
Giant: 
- These are frames more then 1518 bytes that are not jumbo frames

CRC Error:
- these happens when a frame failed the Frame Check sequence 
- Usually indicates a bad cable or bad interface

Encapsulation error:
- This happens when there is inconsistent configurations between switches 







Environmental sensors:
When working with a computer or data center we need to be concerned about the environment 

- temperature: we need to make sure that these devices are constantly cooled and don't get too hot
- Humidity level: we may want to monitor the humidity level in the air has if we have High humidity we could have condensation which could get water on electric equipment and if we have low humidity it could help promote static discharges
- Electricity: since all of these are power devices its also to useful to know if we are receiving the proper amount of voltage and all power is working correct
- Flooding: In large data centers we may use water as part of your cooling system we need maybe have flood monitors to make sure it never gets close to our electrical equipment




After monitoring your network for a while you can start to build a Baseline of your network and see when abnormal events happen







NetFlow:
- SNMP can tell you alot but you may want to know more information about whats in the ethernet packets itself
- NetFlow allows you to get information from the raw traffic traversing the network 
- There's many ways to get this data it may require a seperate individual NetFlow probe or there will be NetFlow built into equipment your using.
- generally there will be a NetFlow probe and a NetFlow collector. 
- The probe will sit on the network sometimes as part of a tapped connection and its watching all the packets traverse the network, gathering the details and exporting them to a NetFlow collector. From the collector you can create reports on the data you get. Allowing you to create extensive reports on network data




Uptime and downtime:
Sometimes it hard to tell if something is Up or down many third party services do this. Alot of status pages do this.