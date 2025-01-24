
Cloud tech brings on demand computing power in a button click


Cloud tech is able to do this at a reasonable cost because cloud providers take advantage of Multitenancy because they have many different clients using the same cloud infrastructure 



Infrastructure as code:
Since most of what is in the code is software based we should be able to define our Infrastructure as code in software. This is where you create code where you can set configurations for switches, Define servers, And you can modify the infrastructures and create versions.
We can also use the code to build other applications instances off the same code so say we need a bunch of routers configured the same way we could just copy paste the code 



Orchestration:
Automation is the key to cloud computing services appear and disappear automatically at the push of a button. 
This is more then building an application and tearing it down automatically. Security policies should also be part of the orchestration and making sure applications are properly provisioned.



Connecting to the cloud:
if you have built a Virtual private cloud on a third party provider but you want that cloud to be private, then your going to need some way to connect to that cloud that doesnt connect to the rest of the internet. One way to do this is by using a Virtual Private Network or VPN. 


There may be times when building out your own virtual private cloud but you would like other people on the internet to have access to be able to do this you should create a  Virtual Private cloud Gateway (VPC) and connect your internet access to the VPC 



VPC endpoints: 
This is a direct direction between cloud provider networks 
![[Screenshot 2024-07-15 001839.png]]



VM sprawl avoidance:
since its so easy to build stuff in a cloud you needs make sure you dont accidently build too many VMs 
![[Screenshot 2024-07-15 002027.png]]


VM escape protection:
There should be no way to escape the virtual machine and get into the host operating system. This is pretty hard for hackers to do so they rlly gotta be l33t Just make sure you keep everything UPDATED SUPER UPDATED SUPER SUPER UPDATED like there is CVEs but like shi be rare 