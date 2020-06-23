---
layout: blog
title: Linux Cheat Sheet
date: 2020-06-22T15:12:51.855Z
thumbnail: uploads/torsten-dederichs-3dda9p4fu9u-unsplash.jpg
---
This guide is made for beginners using Unix-like environments and is terminal focused.
# Table of Contents
1. [Command Line Essentials](#Command-Line-Essentials)
2. [Absolute vs. Relative Paths](#Absolute-vs.-Relative-Paths)
3. [Admin Privileges](#Admin-Privileges)

## Command Line Essentials
What you need to navigate around the terminal.
| cmd            | description                                 |
| -------------- | ------------------------------------------- |
| pwd            | print working directory                     |
| cd             | change directory                            |
| ls             | list contents of current directory          |
| touch \<name>  | make a new file                             |
| mkdir \<name>  | make a directory (i.e. folder)              |
| cp \<what> \<where>| copy a file or directory                |
| mv \<what> \<where>| move a file or directory                |
| mv \<name> \<newName>| rename a file or directory            |
| rm \<path> | delete a file or directory (⚠️)             |
| clear (Ctrl+L) | clear terminal                              |
- **Note**: Both ```cp``` & ```mv``` allow you to rename a file while performing their respective (copy or move) action and can accept full filepaths.
### Extensions of Commands Line Essentials
More complex than the bare essentials, but still essential.
| cmd            | description                                      |
| -------------- | -------------------------------------------------|
| cd ../         | move 1 directory up                              |
| ls \<path>     | list contents of a given directory               |                    
| ls -l          | list contents of directory with permissions (⚠️) |
| rm -r[i] *     | delete the contents of a directory (⚠️)          |
| rm -r[i] \<path>| delete a folder and its contents (⚠️)           |
**Notes**:
- Whenever this guide uses ```[]``` the contents inside of the bracket represent an optional argument.
- The optional argument ```[i]``` triggers ```rm's``` interactive mode which will prompt you before performing each and every delete. This is a safer approach to deletion.
- The author of this guide will like to make note of the  optional ```[f]``` argument (used as -rf) which forcefully deletes a directory or file. While useful this can also be dangerous, please exert caution and ensure you most definitely can and should delete the file or directory before executing this action. 
## Absolute vs. Relative Paths
> "An absolute or full path points to the same location in a file system, regardless of the current working directory. To do that, it must include the root directory. By contrast, a relative path starts from some given working directory, avoiding the need to provide the full absolute path." ([Wikipedia](https://en.wikipedia.org/wiki/Path_(computing)#:~:text=Absolute%20and%20relative%20paths,provide%20the%20full%20absolute%20path.))

| type     | symbol         | description                                |
| -------- | -------------- | ------------------------------------------ |
| absolute | /              | paths beginning from the root directory    |                                   
| relative | omit / (or ./) | paths beginning from the current directory |
| home     | ~              | shortcut to user's home directory          |

## Admin Privileges
| cmd           | description                            |
| ------------- | -------------------------------------- |
| sudo <cmd>    | super user do                          |
| !!            | "bang bang" shorthand for last command |
| su <username> | switch user                            |
| sudo su       | switch to super user                   |
- **Note:** ```!!``` is useful to run a previous command with elevated privileges (e.g. ```sudo !!```)  
## Package Manager (Apt)
**Note:** This part of the guide is only true for Debian based distros that use apt (e.g Ubuntu)
| cmd                                | description                           |
| ---------------------------------- | ------------------------------------- |
| apt-get install <name of program>  | install a program                     |
| apt-get remove <name of program>   | uninstall a program                   |
| apt-cache search <name of program> | search for a program                  |
| apt-cache policy <name of program> | checks if a program is installed      |
| apt-get update                     | updates the package listings          |
| apt-get upgrade                    | upgrades packages with newer versions |

### Installing packages that are not in the repository by manually downloading files:
1. In a web browser, navigate to the download page of the program
2. Download & save the correct package based on your distro and architecture (.deb for Debian)
3. sudo dpkg -i ./<filepath of debian package>

## File Permissions & Ownership
### Understanding file permissions

After running `ls -l` on a directory you should get something like this:

![](/static/uploads/lsTerminal.jpg "privilegeFiles")

For every file name on the far right, there are 3 columns associated with it: its owner, its group, and the public.
The red boxes correspond to the owner, blue to group, and yellow to public.

- d denotes a directory  
- r denotes read permission  
- w denotes write permission  
- x denotes execute permission   

In the case of garden_vintage.jpg, danielmenjivar owns this file and is part of the staff group. danielmenjivar can write and read to this file, the group may read only, and the public may read only.

### Changing ownership
| cmd | description |
| --- | ----------- |
|chown [-R] \<user>:\<group> \<filepath>| change ownership of file (optionally use -R to recursively change ownership of all files inside a directory)|

**Note:** This is useful if a file's permissions are something like this:  
```-rw-r--r--  1 root            staff         0 Jun 22 09:17 landscape.jpg```   
by running: ```sudo chown danielmenjivar:staff landscape.jpg```,   
```danielmenjivar``` now owns the file and can read and write to it.

### Changing permissions 
| cmd | description |
| --- | ----------- |
|chmod [-R] \<new permissions> \<filepath> | modify the file's permissions (or with -R recursively modify all files in a directory)|

New permissions need to be specified for each column (owner, group, public) and are done through numbers:  
- 4 is read only
- 6 is read and write  
this is true for all files, if you're dealing with folders (i.e. directories) just +1 to these.

So, for example full read and write permissions for a file for all groups is 666. Read and write for the owner and the public but only read for the group is 646. If these were directories then 777, and 757 correspondingly. 

## Find and GREP

### Find Command
The find command is used to **search for files** and it's general syntax is:  
```find <directory> [<type>] <search criteria>```  
where: 
- ```<directory>``` is the directory you want to begin searching at
- ```<type>``` is an optional flag, omitting this flag will search for both files and directories
    - ```-type f``` will only search for files
    - ```-type d``` will only search for directories
- a ```search criteria``` such as filename, file permissions, or file size
    - ```-[i]name filename``` search by name with the optional i flag to ignore case sensitivity
    - ```-perm permcode``` search by permissions using a permcode (e.g. 0664)
    - ```-size [+|-]size``` you can search for files greater, lesser, or of exact size (e.g. +1M)
    - Note: you can negate a search criteria by placing the ```-not``` option in front of it.
- Find is recursive, to disable this use ```-maxdepth amount```  where amount is the numeric level (e.g. 1)




