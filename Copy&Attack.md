# Scan A Target
```bash
nmap -A -T5 -sC -sV 10.10.151.254
```
Certainly! Below is the `nmap` command formatted in GitHub Markdown:


## Nmap Scan Command

```bash
nmap -sC -sV -oN nmap/initial 10.10.63.7
```

- **`-sC`**: Enable the default script scan. It runs a set of scripts to gather information about the target and may perform some basic vulnerability checks.

- **`-sV`**: Enable version detection. It attempts to determine the version of the services running on open ports.

- **`-oN nmap/initial`**: Specify the output file name and format. In this case, it's set to save the results in normal format (`-oN`) to a file named `initial` in the `nmap` directory.

- **`10.10.63.7`**: Target IP address that you are scanning.


# Cracking Passwords
```bash
hashcat -O -a 0 -m 20 <password>:<salt> /usr/share/wordlists/SecLists
```
