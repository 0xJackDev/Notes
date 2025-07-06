
Usually if you run

```
nmap -sC -sV *Ip addr* -p- 
```
and you dont get any results try using a friggin UDP scan yo this in a CTF is important .

`sudo nmap -sC -sV *IP* -p- -sU` 
*Keep in mind this will take ALONG time is may be better to target specific UDP ports like 161 for SNMP*



