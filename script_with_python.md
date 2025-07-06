[Black Hat Python](https://github.com/EONRaider/blackhat-python3)

# Table of Contents

- [File Handling with Python](#file-handling) 
- [Python OS Module](#os-module)
- Web Scrapping with Python
    - [Scripting with Request Library](#requests-library)

- Working with Windows PE Files, DLLs, Developing Malware etc
    - [pefiles library](#pefile-library)
    - [Capstone Engine](#capstone-engine-library)
    - [Working with Hex/Int/Bytes](#working-with-hexintbytes)


<hr><br><br><br><br><br>


# File Handling
## Read
### Read The Whole File At Once
```python3
with open(r"D:\bloop\file1.txt.txt", "r") as f:
    data = f.read() # Reads all at once
    print(data)
```
### Read Line by Line
```python3
with open(r"D:\bloop\file1.txt.txt", "r") as f:
    for line in f: # Reads line by line
        print(line) 
```
### Get A List of Strings From The File
```python3
f.readlines()
```

<hr><br><br><br><br><br>

# OS Module
[Full List of Methods and Constants](https://www.w3schools.com/python/module_os.asp)




## Working with Directories:

- `os.getcwd()`: Returns the current working directory.
- `os.chdir(path)`: Changes the current working directory to the specified path.
- `os.listdir(path)`: Returns a list of files and directories in the specified path.
- `os.mkdir(path)`: Creates a new directory at the specified path.
- `os.rmdir(path)`: Removes the directory at the specified path.

Example:

```python
import os

current_directory = os.getcwd()
print("Current Directory:", current_directory)

new_directory = "new_folder"
os.mkdir(new_directory)
os.chdir(new_directory)
print("New Current Directory:", os.getcwd())

file_list = os.listdir(os.getcwd())
print("Files in Current Directory:", file_list)
```

## Working with Files:

- `os.remove(path)`: Removes the file at the specified path.
- `os.rename(src, dst)`: Renames a file or directory from `src` to `dst`.
- `os.path.exists(path)`: Checks if the file or directory at the specified path exists.

Example:

```python
import os

file_path = "example.txt"
with open(file_path, "w") as file:
    file.write("Hello, world!")

os.rename(file_path, "new_example.txt")
print("File exists?", os.path.exists("new_example.txt"))
```

## Executing Shell Commands:

- `os.system(command)`: Executes the shell command in a subshell.

Example:

```python
import os

# Execute a simple shell command
os.system("ls -l")
```

Remember that when dealing with file paths, it's a good practice to use `os.path.join()` to ensure portability across different operating systems.

<hr><br><br><br><br><br>


# Requests Library
**Code 1: Basic Get Request**
```python
import requests

# Basic Get Request
response = requests.get("https://www.facebook.com")
print(response.status_code)
print(response.text)
```

**Code 2: Basic Get with Params**
```python
import requests

# Basic Get with Params
params = {
    "name": "John",
    "age": 25
}

response2 = requests.get("https://httpbin.org/get", params=params)
print(response2.url)
print(response2.text)
```

**Code 3: Basic Post with Payload**
```python
import requests

# Basic Post with Payload
payload = {
    "name": "John",
    "age": 25
}

response_3 = requests.post("https://httpbin.org/post", data=payload)
print(response_3.text)
```

**Code 4: Status Code Verification**
```python
import requests

# Status Code Verification
response_4 = requests.get("https://www.httpbin.org/status/500")
if response_4.status_code == requests.codes.not_found:
    print("Not Found")
else:
    print(response_4.status_code)
```

**Code 5: Changing User Agent**
```python
import requests

# Changing User Agent
headers = {
    "User-Agent": "HelloWorld/1.1"
}
response_5 = requests.get("https://www.httpbin.org/user-agent", headers=headers)
print(response_5.text)
```

**Code 6: Working with Images**
```python
import requests

# Working with Images
headers = {
    "Accept": "image/png"
}

response_6 = requests.get("https://httpbin.org/image", headers=headers)
with open("myimage.png", "wb") as f:
    f.write(response_6.content)
```

**Code 7: Webpage Scanning**
```python
import requests

# Webpage Scanning
for _ in [1, 2, 3]:
    try:
        response = requests.get("https://httpbin.org/delay/8", timeout=3)
    except:
        print("Error in URL: www.example.com/" + str(_))
```

**Code 8: Using a Proxy Server**
```python
import requests

# Using a Proxy Server
proxies = {
    "http": "102.132.38.24:8080",
    "https": "102.132.38.24:8080"
}

response = requests.get("http://httpbin.org/get", proxies=proxies)
print(response.text)
```

<hr><br><br><br><br><br>


# pefile library
## Necessary Functions
### pefile.PE(file_path)
Load the PE file
Example: `pe = pefile.PE(r"C:\Users\vboxuser\projects\capstone-proj-1\benign_hello_world.exe")`
You can even print it and see some real cool stuff
### pe.get_data()

`get_data`(_rva=0_, _length=None_)[](https://pefile.readthedocs.io/en/latest/modules/pefile.html#pefile.PE.get_data "Permalink to this definition")


Get data regardless of its section.

Given a RVA and the size of the chunk to retrieve, this method will find the section where the data lies and return the data.
`get_data()` retrieves the whole section.


## Necessary Values
- Entry Point of the program (RVA) -> `pe.OPTIONAL_HEADER.AddressOfEntryPoint` 
- Where the binary exe is loaded in memory (VA) -> `pe.OPTIONAL_HEADER.ImageBase`
- Code Section Base Address (RVA) -> `pe.OPTIONAL_HEADER.BaseOfCode`

<hr><br><br><br><br><br>

# Capstone-Engine Library
## Necessary Functions
- `disassembler = Cs(CS_ARCH_X86, CS_MODE_32)` -> Initialize the disassembler for x86 32bit system



<hr><br><br><br><br><br>






# Working With Hex/Int/Bytes
# hex to ascii
```python
n.to_bytes(3, byteorder="little").decode()
```

## More work with hex/int/bytes
```python

>>> n.to_bytes(2, byteorder="little")
b'\xa5\x19'


>>> b = bytes.fromhex("414243")
... print(b)          # b'ABC'
...
b'ABC'


>>> n=0x414243
>>> n.to_bytes(3, byteorder="little")
b'CBA'


>>> n.to_bytes(3, byteorder="big")
b'ABC'

```

## From Hex String to Bytes and Converting Back to Hex String

```python
>>> a="6734127789" # Hex String
>>> len(a)
10
>>> bytes.fromhex(a) # Raw Bytes
b'g4\x12w\x89'
>>> b = bytes.fromhex(a)
>>> b.hex() # Convert Back to Hex String
'6734127789'
```

## Extracting Bytes From An Encrypted Hex String and Decrypting Them As A List Item

```python
>>> encrypted="deadbeef" # Suppose, 0xdeadbeef is a super secret encrypted ciphertext
>>> b=bytes.fromhex(encrypted)
>>> b
b'\xde\xad\xbe\xef' # Now they are raw bytes
>>> m=map(hex, list(b)) # map() will take a function and run it over a list. here, list(b)
>>> list(m)
['0xde', '0xad', '0xbe', '0xef']
```


# Malware Obfuscation 
## Very Stupid Obfuscation - Manual

```python
from keystone import *

# Choose architecture + mode
ks = Ks(KS_ARCH_X86, KS_MODE_32)

# Original instructions
orig_code = "xor eax, eax; mov ebx, eax"

# Assemble original code
encoding, count = ks.asm(orig_code)

print("Original code bytes:")
print(bytes(encoding).hex())


# Obfuscated Code
new_code = "pushfd; xor eax, eax; popfd; push eax; pop ebx"

encoding2, count2 = ks.asm(new_code)

print("Obfuscated code bytes:")
print(bytes(encoding2).hex())


# Checking
if len(encoding) == len(encoding2):
    print("Same size, safe replacement!")
else:
    print("Different size! Watch your offsets!")
```


# Quick And Dirty Script (Will Be Moved Later)

```python
>>> y="big" if x > 10 else "small"
>>> y
'big'
>>> a = [1, 2, 3]
>>> a
[1, 2, 3]
>>> b=10 if len(a)>3 else 5
>>> b
5
>>> range(16)
range(0, 16)
>>> bytes(range(16))
b'\x00\x01\x02\x03\x04\x05\x06\x07\x08\t\n\x0b\x0c\r\x0e\x0f'
>>> bytes(range(16)).hex()
'000102030405060708090a0b0c0d0e0f'
>>> print(" ".join(f"{b:02x}" for b in range(16)))
00 01 02 03 04 05 06 07 08 09 0a 0b 0c 0d 0e 0f
```


