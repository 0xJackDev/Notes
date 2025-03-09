

Machine IP :


10.10.11.58


Port 80 and 22 open


Port 80 is using Backdrop CMS Looks like version 1 when looking at the source code

Also there is an exposed .git folder on port 80 as well as robots.txt


i use git-dumper to see this stuff.


grep -Ri 'version' core/


i use this to search for backdrop version and see it is backdrop version 1.27.1


https://www.exploit-db.com/exploits/52021


But for this script I have to  have access to the Backdrop CMS module installer so i assume ill have to get an admin account.



I see a reset password in the next to the login section also on the about page i see the contact is

support@dog.htb 

soo..

