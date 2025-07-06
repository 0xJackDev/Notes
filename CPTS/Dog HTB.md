

Machine IP :

10.129.220.169

Port 80 and 22 open

Port 80 is using Backdrop CMS Looks like version 1 when looking at the source code

Also there is an exposed .git folder on port 80 as well as robots.txt

i use git-dumper to see this stuff.

grep -Ri 'version' core/

i use this to search for backdrop version and see it is backdrop version 1.27.1

[https://www.exploit-db.com/exploits/52021](https://www.exploit-db.com/exploits/52021)

But for this script I have to have access to the Backdrop CMS module installer so i assume ill have to get an admin account.

I see a reset password in the next to the login section also on the about page i see the contact is

[support@dog.htb](mailto:support@dog.htb)

soo..'



Looking at the git database and search for password reset with grep i find a file


core/modules/user/tests/user_password_reset.test



also there is a /files directory

http://dog.htb/.git/logs/refs/heads/master



Looking in here there is a username and password


tiffany user?



tiffany@dog.htb


BackDropJ2024DS2024

password


johncusack:BackDropJ2024DS2024


user
