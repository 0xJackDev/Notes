

openssl s_client -connect 10.129.148.210:imaps

openssl s_client -connect 10.129.148.210:pop3s 

in order to look at the banner of encrypted services.


This is the command i used to retrieve alot of information about the IMAPs server
 curl -k 'imaps://10.129.58.255' --user robin:robin -v



btw you have to put 1 before every command with imap


