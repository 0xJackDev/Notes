

Websites often have subdomains that are not public and won't appear in DNS records. These `subdomains` are only accessible internally or through specific configurations. `VHost fuzzing` is a technique to discover public and non-public `subdomains` and `VHosts` by testing various hostnames against a known IP address

gobuster vhost -u http://planning.htb -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain planning.htb



This fuzzes inlanefreight using name server http://94.237.62.26:37203


gobuster vhost -u http://inlanefreight.htb:51003 -w SecLists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain
