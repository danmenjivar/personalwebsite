---
layout: blog
title: Linux Cheat Sheet
date: 2020-06-22T15:12:51.855Z
thumbnail: uploads/torsten-dederichs-3dda9p4fu9u-unsplash.jpg
---
## Essential Linux Commands
|cmd|description|
|:----:|:-----------------:|
|pwd|print working directory|
|cd|change directory|
|cd ../| move 1 directory up|
|ls|list contents of current directory|
|ls -l|list contents of directory with permissions|
|ls \<dir path>|list contents of a directory| 
|clear (Ctrl+L)|clear terminal|

### A Quick Note on Paths
|type|symbol|description|
|:---:|:-------:|:-----------------:|
|absolute|/|paths beginning from the root directory|
|relative|omit / (or ./)|paths beginning from the current directory|
|home|~|| shortcut to user's home directory|

## Admin Privileges
|cmd|description|
|:----:|:-----------------:|
sudo \<cmd>|super user do|
!!|"bang bang" shorthand for last command|
su \<username>|switch user|
sudo su|switch to super user|

## Apt Package Manager
Note: this is only true for Debian based distros that use apt

|cmd|description|
|:----:|:-----------------:|
|apt-get install \<name of program>|install a program|
|apt-get remove \<name of program>|uninstall a program|
|apt-cache search \<name of program>|search for a program|
|apt-cache policy \<name of program>|checks if a program is installed|





