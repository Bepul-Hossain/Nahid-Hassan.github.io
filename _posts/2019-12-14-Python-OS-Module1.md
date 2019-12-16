---
title: "Python OS module"
date: 2019-12-14
tags: [os.makedirs(), os.listdir(), os.environ]
header:
  image: "/images/os_moudle_1.jpg"
excerpt: "os.makedirs(), os.listdir(), os.environ"
mathjax: "true"
---


[Python | os.makedirs() method](https://www.geeksforgeeks.org/python-os-makedirs-method/)  
OS module in Python provides functions for interacting with the operating system. OS comes under Python’s standard utility modules. This module provides a portable way of using operating system dependent functionality.

All functions in os module raise OSError in the case of invalid or inaccessible file names and paths, or other arguments that have the correct type but are not accepted by the operating system.

**Syntax: os.makedirs(path, mode = 0o777, exist_ok = False**
 
**Parameter:** 

**path:** A path-like object representing a file system path. A path-like object is either a string or bytes object representing a path.  

**mode (optional):** A Integer value representing mode of the newly created directory..If this parameter is omitted then the default value Oo777 is used.  

**exist_ok (optional):** A default value False is used for this parameter. If the target directory already exists an OSError is raised if its value is False otherwise not.  

**Return Type:** This method does not return any value.

# Import os module


```python
import os
```

## os.makedirs() Method


```python
new_directory = "Images/Friend/CSE25"
parent_directory = os.getcwd()

path = os.path.join(parent_directory, new_directory)

os.makedirs(path)
print(path)
```

    /home/nahid/Desktop/Images/Friend/CSE25



```python
ls
```

     [0m[01;34mCRUD-API[0m/          [01;34mDEPT[0m/   [01;34mImages[0m/  'Python OS module.ipynb'
     [01;34mCRUD-API-master[0m/   file    [01;34mOther[0m/    [01;34mSDL_Group_Project[0m/



```python
ls Images/
```

    [0m[01;34mFriend[0m/



```python
ls Images/Friend/
```

    [0m[01;34mCSE25[0m/


### Try to make same directory again...and see the output

```py
new_directory = "Images/Friend/CSE25"
parent_directory = os.getcwd()

path = os.path.join(parent_directory, new_directory)

os.makedirs(path)   
```

### FileExistsError: [Errno 17] File exists: '/home/nahid/Desktop/Images/Friend/CSE25'

### Handling errors while using os.makedirs() method


```python
new_directory = "Images/Friend/CSE25"
parent_directory = os.getcwd()

path = os.path.join(parent_directory, new_directory)

# exit_ok = False
# If the target directory already exists and exit_ok = False then an OSError is raised.

try: 
    os.makedirs(path, exist_ok = False) 
    print("Directory '%s' created successfully" %path) 
except OSError as error: 
    print("Directory '%s' can not be created"%path)

# exit_ok = True
# If the target directory already exists and exit_ok = True then no an OSError is raised.
try: 
    os.makedirs(path, exist_ok = True) 
    print("Directory '%s' created successfully"%path) 
except OSError as error: 
    print("Directory '%s' can not be created"%path)

```

    Directory '/home/nahid/Desktop/Images/Friend/CSE25' can not be created
    Directory '/home/nahid/Desktop/Images/Friend/CSE25' created successfully


## os.listdir()
os.listdir() method in python is used to get the list of all files and directories in the specified directory. If we don’t specify any directory, then list of files and directories in the current working directory will be returned.

**Syntax: os.listdir(path)**

**Parameters:**  

**path (optional):** path of the directory  

**Return Type:** This method returns the list of all files and directories in the specified path. The return type of this method is list.


```python
# Specify the path
list_dir = os.listdir('/') # pass an path string

print(list_dir)
```

    ['lib', 'initrd.img', 'dev', 'etc', 'vmlinuz.old', 'sbin', 'snap', 'srv', 'var', 'root', 'tmp', 'bin', 'home', 'lib64', 'boot', 'lib32', 'mnt', 'proc', 'initrd.img.old', 'lost+found', 'usr', 'sys', 'run', 'opt', 'media', 'vmlinuz', 'cdrom']



```python
# Do not specify the path
print(os.listdir()) # return the current directory file
```

    ['CRUD-API-master', 'Other', '.desktop (1)', 'Images', 'SDL_Group_Project', '.idea', '.ipynb_checkpoints', 'CRUD-API', 'file', 'DEPT', '.desktop', 'Python OS module.ipynb', '.~lock.Demo Lab exam.docx#', '.~lock.Curriculum vitae.rtf#']



```python
ls -a
```

     [0m[01;34m.[0m/                '.desktop (1)'                  '.~lock.Demo Lab exam.docx#'
     [01;34m..[0m/                file                            [01;34mOther[0m/
     [01;34mCRUD-API[0m/          [01;34m.idea[0m/                         'Python OS module.ipynb'
     [01;34mCRUD-API-master[0m/   [01;34mImages[0m/                         [01;34mSDL_Group_Project[0m/
     [01;34mDEPT[0m/              [01;34m.ipynb_checkpoints[0m/
     .desktop          '.~lock.Curriculum vitae.rtf#'


## os.environ()
os.environ in Python is a mapping object that represents the user’s environmental variables. It returns a dictionary having user’s environmental variable as key and their values as value.

**Syntax: os.environ**  

**Parameter:** It is a non-callable object. Hence, no parameter is required  

**Return Type:** This returns a dictionary representing the user’s environmental variables


```python
# using new print method
import pprint

env = os.environ

pprint.pprint(dict(env))
```

    {'CLICOLOR': '1',
     'CLUTTER_IM_MODULE': 'ibus',
     'COLORTERM': 'truecolor',
     'CONDA_DEFAULT_ENV': 'base',
     'CONDA_EXE': '/home/nahid/anaconda3/bin/conda',
     'CONDA_PREFIX': '/home/nahid/anaconda3',
     		     :
		     :
		     :
		     :				
     '_': '/home/nahid/anaconda3/bin/jupyter-notebook',
     '_CE_CONDA': '',
     '_CE_M': ''}


 ### Accessing a particular environment variable


```python
home = os.environ['HOME']
print(home)
```

    /home/nahid



```python
conda_default_env = os.environ['CONDA_DEFAULT_ENV']
conda_default_env
```




    'base'

