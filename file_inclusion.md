# File Inclusion
|-> **Local File Inclusion (LFI)** <br>
|-> **Remote File Inclusion (RFI)** <br>
|-> **Directory Traversal**

<p align="center">
  <img src="https://github.com/PranjalBasak/Documentation/assets/66166653/03a1db1f-9669-4348-9c2b-e9b3056ad3fb" alt="Anatomy of a Get Request to Access a File">
</p>
<p align="center">
  <em>Fig: Anatomy of a Get Request to Access a File</em>
</p>

<p align="center">
  <img src="https://github.com/PranjalBasak/Documentation/assets/66166653/14628d7f-7f11-463f-bb40-ee6bf8154c35" alt="How A Request Works">
</p>
<p align="center">
  <em>Fig: How A Request Works</em>
</p>

**Cause:** 
<br> The main issue of these vulnerabilities is the input validation, in which the user inputs are not sanitized or validated, and the user controls them.
<br>
**Risk:** 
<br> An attacker can access any file in the web server or the operating system including source code using the vulnerablity. 
<br> They can even perform RCE by uploading their own files to the server.

## Path Traversal
AKA _**Directory Traversal/Dot-Dot-Slash Attack**_ <br>
This attack allows a hacker unauthorized access to operating system filee outside the web application's root directory.

In PHP, you can use the [`file_get_contents`](https://www.php.net/manual/en/function.file-get-contents.php) to read the content of a file.

**Example:** `http://webapp.thm/get.php?file=../../../../etc/passwd`

![image](https://github.com/PranjalBasak/Documentation/assets/66166653/eab139b1-d196-46eb-87f7-952d3f212e60)

## Local File Inclusion (LFI)
LFI is a vulnerability which allows attackers to retrive local files hosted in a web server and even execute malicious codes.

LFI can occur in web applications written in PHP, ASP, JSP, or even Node.js. In PHP, some functions contribute to the vulnerability of web applications including `include`, `require`, `include_once`, and `require_once`.

### Case 1:
Let's say we have an web app which can switch between English and Arabian language. The PHP code is written as follows:
```php
<?PHP 
	include($_GET["lang"]);
?>
```

THE PHP code uses a GET request via the URL parameter `lang` to include the file of the page. We should have two kinds of requests:
- `http://webapp.thm/index.php?lang=EN.php`
- `http://webapp.thm/index.php?lang=AR.php`
But a malicious actor can read any file from the server using the vulnerable parameter `lang`, if there is no input validation and no directory specified in the `include` function. So an attacker can do:
`http://webapp.thm/get.php?file=/etc/passwd`
