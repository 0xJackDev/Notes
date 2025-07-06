
Every application that supports authentication mechanisms compares the given entries/credentials with local or remote databases. In the case of local databases these credentials or stored locally on the system. Web applications are often vuln to SQLi which can lead to the worst case scenario a database leak.


There are many different wordlists that contain common password. An example of these lists is rockyou.txt. This contains 14 million unique passwords and was created after a data breach of a company RockYou. The RockYou company stored all the credentials in plain text in their database, which the attackers could view. after a successful SQL injection attack.

We also know that every operating system supports these types of authentication mechanisms. The stored credentials are therefore stored locally. Let's look at how these are created, stored, and managed by Windows and Linux-based systems in more detail.



## Linux
Linux systems handle everything in a file. Passwords are encrypted in a file this is called the shadow file and is at /etc/shadow. and is a part of Linux user management, these passwords are commonly stored in the form of hashes. 
*This /etc/shadow is encrypted so you cannot view it unless your Linux user has permissions to view it which will decrypt it.*

The `/etc/shadow` file has a unique format in which the entries are entered and saved when new users are created.

This is the format. Each thing is separated by :

|   |   |   |   |   |   |   |   |   |
|---|---|---|---|---|---|---|---|---|
|`<username>`:|`<encrypted password>`:|`<day of last change>`:|`<min age>`:|`<max age>`:|`<warning period>`:|`<inactivity period>`:|`<expiration date>`:|`<reserved field>`|

The encryption of the password in this file is formatted as follows:

||||
|---|---|---|
|`$ <id>`|`$ <salt>`|`$ <hashed>`|
|`$ y`|`$ j9T`|`$ 3QSBB6CbHEu...SNIP...f8Ms`|

The type (`id`) is the cryptographic hash method used to encrypt the password. Many different cryptographic hash methods were used in the past and are still used by some systems today.

|**ID**|**Cryptographic Hash Algorithm**|
|---|---|
|`$1$`|[MD5](https://en.wikipedia.org/wiki/MD5)|
|`$2a$`|[Blowfish](https://en.wikipedia.org/wiki/Blowfish_\(cipher\))|
|`$5$`|[SHA-256](https://en.wikipedia.org/wiki/SHA-2)|
|`$6$`|[SHA-512](https://en.wikipedia.org/wiki/SHA-2)|
|`$sha1$`|[SHA1crypt](https://en.wikipedia.org/wiki/SHA-1)|
|`$y$`|[Yescrypt](https://github.com/openwall/yescrypt)|
|`$gy$`|[Gost-yescrypt](https://www.openwall.com/lists/yescrypt/2019/06/30/1)|
|`$7$`|[Scrypt](https://en.wikipedia.org/wiki/Scrypt)|


However a few more files belong to user management system on linux. The other two files are /etc/passwd and /etc/group. 


In the past, the encrypted password was stored together with the username in the `/etc/passwd` file, but this was increasingly recognized as a security problem because the file can be viewed by all users on the system and must be readable. The `/etc/shadow` file can only be read by the user `root`.

#### Passwd File

Credential Storage



The `x` in the password field indicates that the encrypted password is in the `/etc/shadow` file. However, the redirection to the `/etc/shadow` file does not make the users on the system invulnerable because if the rights of this file are set incorrectly, the file can be manipulated so that the user `root` does not need to type a password to log in. Therefore, an empty field means that we can log in with the username without entering a password.

- [Linux User Auth](https://tldp.org/HOWTO/pdf/User-Authentication-HOWTO.pdf)



