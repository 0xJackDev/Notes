
https://legacy.thehacker.recipes/infra/protocols/smb

SMB is server message block it is used and designed for local networks to share files on a "Network drive" at work we use this to deploy software once we join it to a domain without having to have it on thumbdrives. 


if you see port 139 open it probably uses smbv1 which is vuln to the Eternal Blue attack and several more vulnerabilities


if you see port 445 it is using the new smbv2 or v3