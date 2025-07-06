

## Credential Stuffing

There are various databases that keep a running list of known default credentials. One of them is the [DefaultCreds-Cheat-Sheet](https://github.com/ihebski/DefaultCreds-cheat-sheet). Here is a small excerpt from the entire table of this cheat sheet:

We can imagine that we have found some applications used in the network by our customers. After searching the internet for the default credentials, we can create a new list that separates these composite credentials with a colon (`username:password`). In addition, we can select the passwords and mutate them by our `rules` to increase the probability of hits.

#### Credential Stuffing - Hydra Syntax

Password Reuse / Default Passwords

```shell-session
JackTheWizard@htb[/htb]$ hydra -C <user_pass.list> <protocol>://<IP>
```

#### Credential Stuffing - Hydra

Password Reuse / Default Passwords

```shell-session
JackTheWizard@htb[/htb]$ hydra -C user_pass.list ssh://10.129.42.197

...
```

Here, OSINT plays another significant role. Because OSINT gives us a "feel" for how the company and its infrastructure are structured, we will understand which passwords and user names we can combine. We can then store these in our lists and use them afterward. In addition, we can use Google to see if the applications we find have hardcoded credentials that can be used.

#### Google Search - Default Credentials

![Google search results for 'default credentials for tomcat manager' showing a snippet about Apache Tomcat's default blank password for admin.](https://academy.hackthebox.com/storage/modules/147/Google-default-creds.png)

Besides the default credentials for applications, some lists offer them for routers. One of these lists can be found [here](https://www.softwaretestinghelp.com/default-router-username-and-password-list/). It is much less likely that the default credentials for routers are left unchanged. Since these are the central interfaces for networks, administrators typically pay much closer attention to hardening them. Nevertheless, it is still possible that a router is overlooked or is currently only being used in the internal network for test purposes, which we can then exploit for further attacks.

https://www.softwaretestinghelp.com/default-router-username-and-password-list/

it said use the credentials i found last time which was sam:B@tm@n2022!


My question is 

+ 0 Use the user's credentials we found in the previous section and find out the credentials for MySQL. Submit the credentials as the answer. (Format: <username>:<password>)



https://raw.githubusercontent.com/ihebski/DefaultCreds-cheat-sheet/main/DefaultCreds-Cheat-Sheet.csv

mysql -u superdba -p admin 

ended up working