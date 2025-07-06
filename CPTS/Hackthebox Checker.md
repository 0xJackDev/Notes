
Checker box


Machine IP

10.10.11.56


I do a quick port scan and see


port 22


Port 80 
at 
http://checker.htb/login
It is running BookStack login page

Port 8080 

http://checker.htb:8080/

is running

Teampass login

Both 80 and 8080 are running apache servers

After Researching I find a vulnerability on teampass

https://nvd.nist.gov/vuln/detail/CVE-2023-1545


https://security.snyk.io/vuln/SNYK-PHP-NILSTEAMPASSNETTEAMPASS-3367612


Inside that blog there is a poc i run it and get


[haxor@skid pen]$ ./poc.sh http://checker.htb:8080/
There are 2 users in the system:
admin: $2y$10$lKCae0EIUNj6f96ZnLqnC.LbWqrBQCT1LuHEFht6PmE4yH75rpWya
bob: $2y$10$yMypIj1keU.VAqBI692f..XXn0vfyBL7C1EhOs35G59NxmtpJ/tiy
[haxor@skid pen]$



$2y$10$yMypIj1keU.VAqBI692f..XXn0vfyBL7C1EhOs35G59NxmtpJ/tiy:cheerleader



So we have credentials for teampass

bob : cheerleader


Looking more into into stuff I find a bookstack login.

bob@checker.htb

mYSeCr3T_w1kI_P4sSw0rD



ssh access for some reason has an account and password


reader : hiccup-publicly-genesis



So i try to login but I get 
(reader@checker.htb) Verification code:



After looking around I find a way to setup 2fa on Bookstack