

```
ffuf -u http://10.129.240.207 -H "Host: FUZZ.heal.htb" -w SecLists/Discovery/DNS/subdomains-top1million-20000.txt -ac
```

Might need to fuzz for VHOSTS if this doesnt work


Alsol this one good wordlist
```
ffuf -w SecLists/Discovery/DNS/bitquark-subdomains-top100000.txt -u http://planning.htb/ -H "Host: FUZZ.planning.htb" -fs *default size*
```


