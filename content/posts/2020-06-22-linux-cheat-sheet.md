---
layout: blog
title: Linux Cheat Sheet
date: 2020-06-22T15:12:51.855Z
toc: true
featured_image: /uploads/torsten-dederichs-3dda9p4fu9u-unsplash.jpg
featured_image_caption: This guide is made for beginners using Unix-like
  environments and is terminal focused.
---
## Command Line Essentials

The bare essential you need to navigate the terminal.

| cmd                 | description                        |
| ------------------- | ---------------------------------- |
| `pwd`                 | print working directory            |
| `cd`                  | change directory                   |
| `ls`                  | list contents of current directory |
| `touch <name>`        | make a new file                    |
| `mkdir <name>`        | make a directory (i.e. folder)     |
| `cp <what> <where>`   | copy a file or directory           |
| `mv <what> <where>`   | move a file or directory           |
| `mv <name> <newName>` | rename a file or directory         |
| `rm <path>`           | delete a file or directory (⚠️)    |
| `Ctrl+C`              | kill a process (`SIGINT`)          |
| `clear (Ctrl+L)`      | clear terminal                     |
| `man <command>`       | read the manual of a program       |

* **Note**: Both `cp` & `mv` allow you to rename a file while performing their respective (copy or move) action and can accept full filepaths.

### Extensions of Commands Line Essentials

More complex than the bare essentials, but still essential.

| cmd              | description                                          |
| ---------------- | ---------------------------------------------------- |
| `cat <filename>`   | concatenates (useful for viewing files)              |
| `echo <string>`    | outputs string(s) passed (useful for bash scripting) |
| `cd ../`           | move 1 directory up                                  |
| `ls <path>`        | list contents of a given directory                   |
| `ls -l`            | list contents of directory with permissions (⚠️)     |
| `rm -r[i] *`      | delete the contents of a directory (⚠️)              |
| `rm -r[i] <path>` | delete a folder and its contents (⚠️)                |
| `Ctrl+Z`           | suspend a process (`SIGSTOP`)                        |
| `script <output>`  | log terminal to a file                               |

**Notes**:

* Whenever this guide uses `[]` the contents inside of the bracket represent an optional argument.
* The optional argument `[i]` triggers `rm's` interactive mode which will prompt you before performing each and every delete. This is a safer approach to deletion.
* The author of this guide will like to make note of the  optional `[f]` argument (used as -rf) which forcefully deletes a directory or file. While useful this can also be dangerous, please exert caution and ensure you most definitely can and should delete the file or directory before executing this action. 

## Absolute vs. Relative Paths

| type     | symbol         | description                                |
| -------- | -------------- | ------------------------------------------ |
| absolute | `/`              | paths beginning from the root directory    |
| relative | omit `/` (or `./`) | paths beginning from the current directory |
| home     | `~`              | shortcut to user's home directory          |

## Admin Privileges

| cmd           | description                            |
| ------------- | -------------------------------------- |
| `sudo <cmd>`    | super user do                          |
| `!!`            | "bang bang" shorthand for last command |
| `su <username>` | switch user                            |
| `sudo su`       | switch to super user                   |

* **Note:** `!!` is useful to run a previous command with elevated privileges (e.g. `sudo !!`)  

## Package Manager (apt)

**Note:** This part of the guide is only true for Debian based distros that use apt (e.g Ubuntu)

| cmd                     | description                           |
| ----------------------- | ------------------------------------- |
| `apt install <name>`  | install a program                     |
| `apt remove <name>`   | uninstall a program                   |
| `apt search <name>` | search for a program                  |
| `apt policy <name>` | checks if a program is installed`      |
| `apt update`          | updates the package listings          |
| `apt upgrade`         | upgrades packages with newer versions |

**Note:** It’s not uncommon to chain update and upgrade by running `apt update && apt upgrade`. `&&` is used to chain commands together if and only the previous command exited without errors.

### Installing packages not in the repository by manually downloading files:

1. In a web browser, navigate to the download page of the program
2. Download & save the correct package based on your distro and architecture (.deb for Debian)
3. Run `sudo dpkg -i ./<path>` where `<path>` is the filepath of the debian package (e.g .deb)

## File Permissions & Ownership

### Understanding File Permissions

After running `ls -l` on a directory you should get something like this:

![](/uploads/lsTerminal.jpg)

The 3 columns on the left represent 3 associations every file/directory has:

* <span style=“color:red”>user</span> (i.e. the owner of the file/directory) \[red]
* group  \[blue]
* other (i.e. the public, the “world)  \[yellow]

The letters represent file permissions:

* `r` = read permission  
* `w` = write permission  
* `x` = execute permission
* and the prefix `d` = directory     

In the case of `garden_vintage.jpg`, `danielmenjivar` owns this file and is part of the `staff` group.\
`danielmenjivar` can write and read to this file, both the `staff` group and the public may read only.

### Changing Ownership (chown)

| cmd                               | description      |
| --------------------------------- | ---------------- |
| `chown [-R] <user>:<group> <path>` | change ownership |

**Note:** The optional argument \[-R] is used to recursively change ownership of all files inside a directory. 

**Why/When do we use chown?** A common scenario to use `chown` is when certain files or directories are owned by the root user and need to be owned by another non-root user. In this scenario a file's permission would look something like this (after executing `ls -l`):\
`-rw-r--r--  1 root            staff         0 Jun 22 09:17 landscape.jpg`.\
By executing: `sudo chown danielmenjivar:staff landscape.jpg`,\
`danielmenjivar` gains ownership the file and as a result can read and write to it.

### Modifying Permissions (chmod)

| cmd                            | description                   |
| ------------------------------ | ----------------------------- |
| `chmod [-R] <shorthand> <path>` | modify the file's permissions |

**Note:** The optional argument \[-R] is used to recursively modify permissions of all the files inside a directory.

#### chmod using shorthands (recommended)

| groups               | permissions              | operator               |
| -------------------- | ------------------------ | ---------------------- |
| u = user             | x = execute              | + Add                  |
| g = group            | w = write                | \- Remove              |
| o = other            | r = read                 | \= Equals              |
| a = all of the above | (blank) = no permissions | , to chain assignments |

**Example**
To assign an user read & write, add write to group, and assign no permissions to other.

`chmod u=rw,g+w,o=`

#### chmod using octals (harder)

Octal permissions are set using numbers from `0` to `7`.

All you need to know are the basics:

| octal base | permissions |
| ---------- | ----------- |
| 0          | none        |
| 1          | execute     |
| 2          | write       |
| 4          | read        |

From there, the rest are just combinations (sums)

| combo permission       | sum           |
| ---------------------- | ------------- |
| execute + write        | 1 + 2 = 3     |
| execute + read         | 1 + 4 = 5     |
| write + read           | 2 + 4 = 6     |
| execute + write + read | 1 + 2 + 4 = 7 |

**Tip:** if the number is **odd**, it includes **execute**

| cmd                      | description                   |
| ------------------------ | ----------------------------- |
| `chmod [-R] <ugo> <path>` | modify the file's permissions |

Where `ugo` is the corresponding user mapped to an octal (user, group, other).

**Example**
To give read/write permissions to user, read to group, and none to others you’d run:

`chmod 640 file`

**Note:** The optional argument \[-R] is used to recursively modify permissions of all the files inside a directory.

**Why/When/How do we use chmod?** Suppose you are an admin and a staff member (who is part of the `staff` group) wants to edit `file.txt`, but for some odd reason they can't. To investigate they run `ls -l` and this is the result:
`-rw-r--r--  1 danielmenjivar  staff  0 Jun 23 11:56 file.txt`.
The staff members ask you give them read-and-write permission. You don't want the public to be able to read-and-write and there is no need to give them ownership of `file.txt`. To do this, all you have to do is run:
`chmod 664 ./file.txt`, where 6 is read-and-write for yourself (no reason to give up these permissions for yourself, let's assume you are me `danmenjivar`, the owner), 6 is read-and-write for the staff group, and 4 is read only for the public (you don't want any shenanigans happening). Every column gets a number, for more details on chmod check out the `man` page on it.

## Find and Grep

### Find

| cmd                                  | description      |
| ------------------------------------ | ---------------- |
| `find <directory> [<type>] <criteria>` | search for files |

* `<directory>` is the path of the directory you want to begin searching at
* `<type>` is an optional flag, omitting this flag will search for both files and directories

  * `-type f` will only search for files
  * `-type d` will only search for directories
* a search `<criteria>` such as filename, file permissions, or file size

  * `-[i]name <filename>` search by name with the optional `[i]` flag to ignore case sensitivity
  * `-perm mode` search by permissions using a mode (e.g. 0664)
  * `-size [+|-]size` you can search for files greater, lesser, or of exact size (e.g. +1M, -1M, 1M)
  * **Note:** you can negate a search criteria by placing the `-not` option in front of the criteria.
* Find is recursive by default, to disable this use `-maxdepth <amount>`  where `<amount>` is the numeric level (e.g. 1) to limit your search.

### Grep

| cmd                                    | description              |
| -------------------------------------- | ------------------------ |
| `grep [-n] [-i] <keyword> <directory>` | search contents of files |

* `<directory>` is the path of the directory you want to begin searching at
* `<keyword>` is the search string, i.e. what you're looking for
* `[-i]` optional flag, ignores case sensitivity
* `[-n]` optional flag, appends the line numbers to each result

### Grep+Find

| cmd                                                                                             | description                              |
| ----------------------------------------------------------------------------------------------- | ---------------------------------------- |
| `find <directory> [<type>] <criteria> -exec grep [-n] [-i] <keyword> <directory> {} +`| search contents of some particular files |

* `-exec` joins the find and grep commands
* `{} +` is used to delimit the end of the `-exec`

**When/How/Why?** Suppose you want to search for the contents of some php files in your current directory. The find command for searching php files would be: `find . -type -iname "*.php"`. To search the contents of these files you can pair find with grep using the `-exec` command. All `-exec` does is run your grep command after running find. To signal when the exec is over, we append `{} +` to the end of the grep command. The resulting command would look like this: `find . -type -iname "*.php" -exec grep -i -n "function" {} +`.

## Redirecting Output of a Command

| cmd                  | description          |                                                                          
| -------------------- | ------------------------------ | 
| `<cmd> | <cmd>` | pipes transfers output from the command on its left into the standard input of the command on its right | 
| `<command> > <output>` | redirect the output of the command on the left to the file on the right (e.g. ls > out.txt) [2 |                
| `<cmd> >> <output>` | redirect output of a command on the left and append it to the end of the file on the right |     
| `<cmd> < <input>` | read from a file |                                                           
| `<command> | tee <output>` |                                    redirecting output of a command while seeing results in real-time (e.g. `ls | tee out.txt`) |

**Note:** Apart from redirecting between apps & files, we can also redirect between streams by specifying a POSIX stream ID. The `>` by itself is redirecting standard output (i.e. stream ID 1). For example, we can redirect standard error like this: `<cmd> 2> <output>` where 2 indicates the POSIX stream ID. To redirect both standard output and error we’d use `<cmd> &> <output>`. Note that `>` and `1>` are identical since the default behavior of redirect is to do so on standard output.

| POSIX stream ID      | description                    |                                                                          
| -------------------- | ------------------------------ | 
| 0 | standard input | 
| 1 | standard output |
| 2 | standard error | 

## Manage Processes (top)

| cmd               | description                                                    |
| ----------------- | -------------------------------------------------------------- |
| `top`               | shows in real-time the top of the list of running applications |
| `ps aux`            | captures a list of running applications (not real-time)        |
| `pgrep <command>`   | lists the pid's associated with a command                      |
| `kill <pid>`        | kill a process instance                                        |
| `killall <command>` | kill all instances of a process                                |

**Notes:** 

* `top`:

  * `PID` is the process id, used to manage processes
  * `USER` who the process is running for
  * `TIME+` how long the process has been running for
  * `COMMAND` the command associated with the process
* `ps aux`:

  * You can use grep to search for processes like this: `ps aux | grep firefox`
* `pgrep`:

  * the pid's are listed in chronological order

**Tip:** You can run commands in the background by post fixig the `&` command. This can be useful for opening applications (e.g. `firefox &`) or running several commands inside one ssh shell.

## Services

Services are background processes. 

| cmd                    | description       |
| ---------------------- | ----------------- |
| `service <name> start`   | start a service   |
| `service <name> stop`    | stop a service    |
| `service <name> restart` | restart a service |
| `systemctl start <name>` | start a service   |
| `systemctl stop <name>`  | stop a service    |

## Scheduling Tasks (crontab/cronjobs)

Cronjobs are processes used to automate tasks (e.g. running backups, updates, etc.)

| cmd        | description                        |
| ---------- | ---------------------------------- |
| `crontab -e` | start a ctrontab & save it to /etc |

### Cronjob Structure

| abbreviation | meaning      | values |
| ------------ | ------------ | ------ |
| m            | minutes      | 0-59   |
| h            | hours        | 0-23   |
| dom          | day of month | 1-31   |
| mon          | month number | 1-12   |
| dow          | day of week  | 0-6    |
| command      | to perform   |        |

## Managing Users

| cmd                            | description                          |
| ------------------------------ | ------------------------------------ |
| `adduser <username>`             | add new user                         |
| `adduser <username> sudo        | add user to sudo group`               |
| `deluser <username>`             | remove user                          |
| `passwd <username>`              | change a password for a user account |
| `groupadd <groupname>`           | create a new group                   |
| `adduser <username> <groupname>` | add user to group                    |
| `deluser <username> <groupname>` | remove user from group                    |

## History: Running Past Commands

| cmd     | description                                |
| ------- | ------------------------------------------ |
| `!!`      | "bang bang", shorthand for last command    |
| `history` | displays the last couple commands ran      |
| `!<line>` | run past command based on a command number |

**Tip:** Ran a command that needs sudo without it? Just run `sudo !!`.

## Fun Terminal Commands

| cmd               | description                                     |
| ----------------- | ----------------------------------------------- |
| `figlet`            | turn boring text into fancy big text            |
| `fortune`           | generate random messages                        |
| `cowsay`            | because everything is better when a cow says it |
| `cowsay -f moofasa` | turn cow into ’moofasa’                         |
| `lolcat [-a]`      | rainbow print concatenation \[animate]          |
| `sl`                | steam train coming through                      |
| `cmatrix`           | become the chosen one                           |