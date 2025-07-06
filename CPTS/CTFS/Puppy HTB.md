


So I started by enumurating SMB shares with netexec

```

[haxor@skid Fuzz]$ nxc smb 10.10.11.70 -u levi.james -p 'KingofAkron2025!' --shares
SMB         10.10.11.70     445    DC               [*] Windows Server 2022 Build 20348 x64 (name:DC) (domain:PUPPY.HTB) (signing:True) (SMBv1:False)
SMB         10.10.11.70     445    DC               [+] PUPPY.HTB\levi.james:KingofAkron2025!
SMB         10.10.11.70     445    DC               [*] Enumerated shares
SMB         10.10.11.70     445    DC               Share           Permissions     Remark
SMB         10.10.11.70     445    DC               -----           -----------     ------
SMB         10.10.11.70     445    DC               ADMIN$                          Remote Admin
SMB         10.10.11.70     445    DC               C$                              Default share
SMB         10.10.11.70     445    DC               DEV                             DEV-SHARE for PUPPY-DEVS
SMB         10.10.11.70     445    DC               IPC$            READ            Remote IPC
SMB         10.10.11.70     445    DC               NETLOGON        READ            Logon server share
SMB         10.10.11.70     445    DC               SYSVOL          READ            Logon server share




```


So the smb shares are

ADMIN$
C$
DEV       // DEV SHARE FOR PUPPY DEVS
IPC$       ;READ
NETLOGON    ;READ 
SYSVOL    ; READ




then ok let me do nmap scan



So the domain is puppy.htb I assume the DC is the IP my nmap scan confirms this as it is running ldap, dns, kerberos . also WinRM is enabled on this machine 


```


[haxor@skid pen]$ nxc ldap 10.10.11.70 -u levi.james -p KingofAkron2025!
LDAP        10.10.11.70     389    DC               [*] Windows Server 2022 Build 20348 (name:DC) (domain:PUPPY.HTB)
LDAP        10.10.11.70     389    DC               [+] PUPPY.HTB\levi.james:KingofAkron2025!
```


ldap credentials work sooo lets I guess learn how to use bloodhound.


