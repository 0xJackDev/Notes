
on your network you have probably installed switches routers and firewalls. But how do you know if those devices are performing well. There are a number of Performance metrics that will give you information about how well these devices are performing 


For example 
- Temperature, Alot of devices has internal sensors for temperature so you can measure the temp of the CPU/GPU. If you start to notice a trend where temp is rising or seems higher then normal this can be a early warning of excessive utilization or hardware issues or software issues
- CPU usage, This another important metric that measures the performance of the processor(s), the Overall performance is gonna usually be based on this value
- Memory, We wanna make sure that we have plenty of memory available for all process because this is the operational resource and say if we ran out of memory, our system would usually crash or at least the application.







Bandwidth Monitor:
- Most of the devices you monitor are somehow connected to the Network and usually these devices are forwarding/passing traffic from one Network to another. Having some way to monitor the bandwidth is vital 
- There are a number of ways to do this a easy way would be with SNMPv3, There are other more advanced methods like NetFlow, Sflow or IPFIX. You could also capture packets yourself with tools like Wireshark or use a software agent to help you. 
- If you see that the utilization is getting above 85% or 90% This is an early warning that there is no more available space on the network. and a large amount of traffic is traversing this link.





Latency:
- This is the delay between a request is a response 
- The waiting time between request and response 
- Some latency is expected and normal because of the laws of physics
- The farther the data is going the longer the Latency will be.
- If you are confused on why network is slow is may be useful to send a packet and examine the Latency at every step along the way 
- Packet captures can provide detailed analysis





Jitter:
We deal with alot of real time media on our networks, most of this is VOIP traffic or video traffic.
If you lose a packet of Real-time data then theres no way for retransmission
- Jitter is the time between frames, Excessive jitter can cause you to miss information with "choppy" voice calls.






Monitoring the interface:
this is very important you are able to monitor these individual network interfaces on these devices 
- Often this is the first sign of trouble and can give you more insight into potential problems 
- For example a small number of errors might indicate a bigger issue like a problem with a switch or a congestion in the network
- We can do this monitoring with SNMP, SNMP allows us to query the statistics of a device and the device will respond back will the statistics and you can continue to do that over time to build a trend. 
- Many of the devices will have a very standard Database we use for this statistics in SNMP we call this a Management Information base or a (MIB) one type of standard MIB is MIB-2. You should be able to query MIB-II with MIB-2 queries and it will respond in MIB-2 format. 
- Many devices will include their own proprietary MIB for example a firewall, switch or printer will have specific metrics for firewalls, printers or switches 



One basic status to monitor is whether or not a interface is active. Is the link up or down.

We also wanna monitor these systems to see if any ERRORS are occurs we can check CRC errors, RUNT and GIANT

we can check Network Utilization and CPU/GPU utilization. And we can run bandwidth tests to view throughput 