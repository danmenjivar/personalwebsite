---
layout: blog
title: Linux Cheat Sheet
date: 2020-06-22T15:12:51.855Z
thumbnail: uploads/torsten-dederichs-3dda9p4fu9u-unsplash.jpg
---
![]()

Note: this guide is made for beginners and is Debian/Ubuntu focused.

## Essential Linux Commands

| cmd            | description                                 |
| -------------- | ------------------------------------------- |
| pwd            | print working directory                     |
| cd             | change directory                            |
| cd ../         | move 1 directory up                         |
| ls             | list contents of current directory          |
| ls -l          | list contents of directory with permissions |
| ls \<dir path>  | list contents of a directory                |
| rm \<filepath> | delete a file|
|rm -r[i] *| deletes all the contents of a folder (with optional i flag asks before deleting each item)|
|rm -r[i] \<filepath>| delete a folder and its contents (optional i will asks before deleting each file)|
| mkdir \<name> |make a folder|
| touch \<filename>| make a new file|
|cp 
| clear (Ctrl+L) | clear terminal                              |

### A Quick Note on Paths

| type     | symbol         | description                                |                                   |
| -------- | -------------- | ------------------------------------------ | --------------------------------- |
| absolute | /              | paths beginning from the root directory    |                                   |
| relative | omit / (or ./) | paths beginning from the current directory |                                   |
| home     | ~              |                                           shortcut to user's home directory |

## Admin Privileges

| cmd           | description                            |
| ------------- | -------------------------------------- |
| sudo <cmd>    | super user do                          |
| !!            | "bang bang" shorthand for last command |
| su <username> | switch user                            |
| sudo su       | switch to super user                   |

## Apt Package Manager

Note: this is only true for Debian based distros that use apt

| cmd                                | description                           |
| ---------------------------------- | ------------------------------------- |
| apt-get install <name of program>  | install a program                     |
| apt-get remove <name of program>   | uninstall a program                   |
| apt-cache search <name of program> | search for a program                  |
| apt-cache policy <name of program> | checks if a program is installed      |
| apt-get update                     | updates the package listings          |
| apt-get upgrade                    | upgrades packages with newer versions |

### Installing packages that are not in the repository by manually downloading files

1. In a web browser, navigate to the download page of the program
2. Download & save the correct package based on your distro and architecture (.deb for Debian)
3. sudo dpkg -i ./<filepath of debian package>

## File Permissions & Ownership

### Understanding file permissions

After running `ls -l` on a directory you should get something like this:

![](uploads/screen-shot-2020-06-22-at-9.03.07-am.jpg "privilegeFiles")

For every file name on the far right, there are 3 columns associated with it: its owner, its group, and the public.
The red boxes correspond to the owner, blue to group, and yellow to public.

d denotes a directory  
r denotes read permission  
w denotes write permission  
x denotes execute permission   

In the case of garden_vintage.jpg, danielmenjivar owns this file and is part of the staff group. danielmenjivar can write and read to this file, the group may read only, and the public may read only.

### Changing ownership
| cmd | description |
| --- | ----------- |
|chown [-R] \<user>:\<group> \<filepath>| change ownership of file (optionally use -R to recursively change ownership of all files inside a directory)|

This is useful if a file is something like this ```-rw-r--r--  1 root            staff         0 Jun 22 09:17 landscape.jpg``` by running ```sudo chown danielmenjivar:staff landscape.jpg```, I  now own the file and can read and write to it.

### Changing permissions 
| cmd | description |
| --- | ----------- |
|chmod [-R] \<new permissions> \<filepath> | modify the file's permissions (or with -R recursively modify all files in a directory)|

New permissions need to be specified for each column (owner, group, public) and are done through numbers:  
- 4 is read only
- 6 is read and write  
this is true for all files, if you're dealing with folders (i.e. directories) just +1 to these.

So, for example full read and write permissions for a file for all groups is 666. Read and write for the owner and the public but only read for the group is 646. If these were directories then 777, and 757 correspondingly. 




