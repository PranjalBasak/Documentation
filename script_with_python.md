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

# OS Module
[Full List of Methods and Constants](https://www.w3schools.com/python/module_os.asp)
