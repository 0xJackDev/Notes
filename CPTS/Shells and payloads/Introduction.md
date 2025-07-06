

A shell is a program that provides a user on a computer with an interface to input instruction into the system and view text output 

Bash, ZSH




Since a shell gives us direct access to a command line on a computer it gives us access to everything running under the user running the shall. (AKA THE USER WHO EXECUTED /BIN/BASH)


#### No. 2: Client - Connecting to bind shell on target

Bind Shells

```shell-session
JackTheWizard@htb[/htb]$ nc -nv 10.129.41.200 7777

Target@server:~$  
```



There are more custom configured shells for security like.

just type echo $SHELL (usually ig)


You can also find this out from the ps command and the env command





## Bind Shells


in many cases, we will be working establish a shell on a system on a local or remote network. This means we will be looking to use the terminal emulator application on our local attack box to control the remote system through its shell. This is typically done using a Bind and Reverse Shell

## What Is It?

With a bind shell, the `target` system has a listener started and awaits a connection from a pentester's system (attack box).

#### Bind Example

![image](https://academy.hackthebox.com/storage/modules/115/bindshell.png)

As seen in the image we would connect directly with the IP address and port listening on the target. There can be many challenges with getting the shell with way though


- The listener has to be started on the Target machine 
- Admins typically configure strict incoming firewall rules and NAT at the edge of the network, so we would likely have to be on the internal network to be able to pivot like this.
- Operating system firewalls will likely block most incoming connections that are trusted



OS firewalls become a real issue when establishing a shell since we need to consider IP addresses, ports, and the tool in use to get our connection working. In the example above the application used to start the listener is Netcat.


