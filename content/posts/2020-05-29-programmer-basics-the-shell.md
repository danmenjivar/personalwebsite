---
layout: blog
title: "Programmer Basics: The Shell"
date: 2020-05-29T18:09:32.246Z
thumbnail: uploads/blur-bright-business-codes-207580-1-.jpg
---
## What is the shell?

A shell is nothing more but a computer program that allows you to control your computer using only keyboard commands and nothing else.

Given that most tasks can be accomplished using a GUI (Graphical User Interface), you may be asking yourself why bother using the shell at all.  

## Why use the shell?

CLI's (Command Line Interfaces) unlock full control of your computer. Think about it, there is only so many buttons and windows you can display on a screen at a given moment. This limits the options available, but interacting with your computer the old-school ways strips away these limitations.

Almost all platforms nowadays ship with some form of shell. Most of these even contain multiple shells to choose from. But, their purpose is the same. They provide a CLI for you to access OS services. This means running programs, accepting input, and displaying output. 

In this post, our focus will be on bash. Bash is short for the Bourne Again Shell and is very widely used. To open a shell prompt, you'll need a terminal. More likely than not your computer already has one pre-installed.

### Shell basics

Okay, so off the bat when you run your terminal you should see a prompt like this: 

`dmenj:~$`

* *dmenj* tells you the name of the machine you are on
* *the information following the colon (:)* tells you your current working directory (cwd), ~ is shorthand for your home directory
* $ tells you 2 things:

  * you are not the root user
  * the shell is prompting you for a command

### Running programs

To run a program from the shell, simply type the program's name and hit return 

`dmenj:~$ date
Fri May 29 11:41:11 PDT 2020
dmenj:~$`

The date command executes the date program which prints the current date & time. We can also run a command that takes input, i.e. arguments as follows:

`dmenj:~$ echo hello
hello`

The echo command runs the program echo which takes any arguments given to it, splits these arguments on whitespace and then prints them back to the terminal. To pass arguments with special characters quotes or escape sequences are required.