# Scan A Target
```bash
nmap -A -T5 -sC -sV 10.10.151.254
```

# Cracking Passwords
```bash
hashcat -O -a 0 -m 20 <password>:<salt> /usr/share/wordlists/SecLists
```
