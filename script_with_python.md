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




# Working with Directories:

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

# Working with Files:

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

# Executing Shell Commands:

- `os.system(command)`: Executes the shell command in a subshell.

Example:

```python
import os

# Execute a simple shell command
os.system("ls -l")
```

Remember that when dealing with file paths, it's a good practice to use `os.path.join()` to ensure portability across different operating systems.
```
