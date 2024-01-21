# Reconnaissance
## Passive Reconnaissance
- whois
- nslookup
- dig

- `whois domain`
- `nslookup -type=A tryhackme.com 1.1.1.1`
- `dig @1.1.1.1 tryhackme.com MX`

- `DNSDumpster` : A Website that Finds out subdomains of a domain
- `shodan.io` : Gives us the following information on a website:
  - IP address
  - hosting company
  - geographic location
  - server type and version

| Purpose                      | Commandline Example                     |
|------------------------------|-----------------------------------------|
| Lookup WHOIS record          | `whois tryhackme.com`                   |
| Lookup DNS A records         | `nslookup -type=A tryhackme.com`        |
| Lookup DNS MX records at DNS server | `nslookup -type=MX tryhackme.com 1.1.1.1` |
| Lookup DNS TXT records        | `nslookup -type=TXT tryhackme.com`      |
| Lookup DNS A records          | `dig tryhackme.com A`                   |
| Lookup DNS MX records at DNS server | `dig @1.1.1.1 tryhackme.com MX`      |
| Lookup DNS TXT records        | `dig tryhackme.com TXT`                 |

### Active Reconnaissance
- Web Browser
  - FoxyProxy
  - User-Agent Switcher and Manager
  - Wappalyzer
- ping ( `ping -c 10 <host>` )
- traceroute
- telnet
- netcat

**Note:** TTL indicates the maximum number of routers/hops that a packet can pass through before being dropped; TTL is not a maximum number of time units.

#### Telnet
```bash
telnet <ip> <port>
```
One can use telnet to access any service running on TCP and even exchange messages unless it uses encryption.
After connecting, we can send

```bash
GET / HTTP/1.1
host:telnet
```
This way we can grab banners of a service or a system.

#### Netcat
Netcat will create a simple TCP/UDP server or client. Whatever you type on client side will be echoed to server side and vice versa. Netcat is a simple way to grab a banner.

**Start A Listener/Server:**
```bash
nc -lvnp <port>
```

**Connect to A Server:**
```bash
nc <ip> <port>
```
Afterwards:
```bash
GET / HTTP/1.1
host: netcat
```

| Option | Meaning                                      |
|--------|----------------------------------------------|
| -l     | Listen mode                                  |
| -p     | Specify the Port number                      |
| -n     | Numeric only; no resolution of hostnames via DNS |
| -v     | Verbose output (optional, yet useful to discover any bugs) |
| -vv    | Very Verbose (optional)                      |
| -k     | Keep listening after client disconnects      |

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
