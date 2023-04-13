---
title: "Shell basics handbook"
seoTitle: "Shell basics handbook"
seoDescription: "A shell is a program that acts as an interface between a user and the kernel. It allows a user to give commands to the kernel and receive responses from it."
datePublished: Thu Apr 13 2023 21:25:07 GMT+0000 (Coordinated Universal Time)
cuid: clgfmpprd000c09jugft8h3rs
slug: shell-basics-handbook
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/6RTn6HZD-RI/upload/94b466d9a41d413dbf66ce2d5c0bb8e4.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1681421055429/61bbd7ed-682b-4402-be9e-bc5bbe39075d.jpeg
tags: linux, terminal, bash, shell, shebang

---

> [Buy me a coffee](https://linktr.ee/joehsn) ☕ to help me keep going, thanks in advance! ❤

A shell is a program that acts as an interface between a user and the kernel. It allows a user to give commands to the kernel and receive responses from it. Through a shell, we can execute programs and utilities on the kernel. Hence, at its core, a shell is a program used to execute other programs on our system. It is responsible for the control management, and execution of processes, and ensuring proper utilization of system resources.

Being able to interact with the kernel makes shells a powerful tool. Without the ability to interact with the kernel, a user cannot access the utilities offered by their machine’s operating system.

# What's a "Terminal?"

It's a program called a *terminal emulator*. This is a program that opens a window and lets you interact with the shell. There are a bunch of different terminal emulators we can use. Some Linux distributions install several.

These might include `gnome-terminal`, `konsole`, `xterm`, `rxvt`, `kvt`, `nxterm`, and `eterm`.

In Linux, you can navigate your filesystem using the shell prompt. Navigation is based on the concept of paths. These paths specify what directories to traverse to reach a particular subdirectory or file. There are two types of paths: Absolute paths and relative paths.

In the Linux shell, the `$` and `#` Symbols have different meanings. The `$` symbol is used to indicate that you are logged in as a regular user. The `#` symbol is used to indicate that you are logged in as the root user.

> In Linux, the root user is the most powerful user on a Unix/Linux system.
> 
> File names in Linux, like Unix, are case-sensitive. "File1" and "file1" refer to different files.
> 
> **Most importantly, do not embed spaces in file names**. If you want to represent spaces between words in a file name, use underscore characters. You will thank yourself later.

# **Working with Commands**

we’ll see several commands and their mysterious options and arguments. We will try to remove some of that mystery using the following commands.

Most commands operate like this:

```bash
command -options arguments
```

## **What are "Commands?"**

Commands can be one of 4 different kinds:

1. **An executable program** like all those files we saw in `/usr/bin`. Within this category, programs can be *compiled binaries* such as programs written in C and C++, or programs written in *scripting languages* such as the shell, Perl, Python, Ruby, etc.
    
2. **A command is built into the shell itself.** bash provides several commands internally called *shell built-ins*. The `cd` command, for example, is a shell built-in.
    
3. **A shell function.** These are miniature shell scripts incorporated into the *environment*. We will cover configuring the environment and writing shell functions in later lessons, but for now, just be aware that they exist.
    
4. **An alias.** Commands that we can define ourselves, are built from other commands. This will be covered in a later lesson.
    

### `type` (displays the kind of command the shell will execute)

It is often useful to know exactly which of the four kinds of commands is being used.

```bash
[me@linuxbox me]$ type cp
```

### `which` **(determines the exact location of a given executable)**

Sometimes there is more than one version of an executable program installed on a system. While this is not very common on desktop systems, it's not unusual on large servers.

```bash
[me@linuxbox me]$ which ls
```

> `which` only works for executable programs, not built-ins nor aliases that are substitutes for actual executable programs.

## **Getting Command Documentation**

With this knowledge of what a command is, we can now search for the documentation available for each kind of command.

### `help` (a built-in facility available for each of the shell built-ins)

we can add the `-m` option to change the format of the output.

```bash
[me@linuxbox me]$ help -m cd
```

> A note on notation: When square brackets appear in the description of a command's syntax, they indicate optional items. A vertical bar character indicates mutually exclusive items. In the case of the cd command above:
> 
> ```bash
> cd [-L|-P] [dir]
> ```

### `--help` (an option that displays a description of the command)

Many executable programs support a `--help` option. For example:

```bash
[me@linuxbox me]$ mkdir --help
```

### `man` (an interface to the system reference manuals)

Most executable programs intended for command line use provide a formal piece of documentation called a *manual* or *man page*. A special paging program called `man` is used to viewing them.

```bash
man command
```

> On most Linux systems, `man` uses `less` to display the manual page, so all of the familiar `less` commands work while displaying the page.
> 
> Man pages vary somewhat in format but generally contain a title, a synopsis of the command's syntax, a description of the command's purpose, and a listing and description of each of the command's options. Man pages, however, do not usually include examples, and are intended as a reference, not a tutorial.

## README and Other Documentation Files

Many software packages installed on your system have documentation files residing in the `/usr/share/doc` directory. Most of these are stored in plain text format and can be viewed with `less`. Some of the files are in HTML format and can be viewed with a web browser.

# Keyboard shortcuts for Bash

The bash shell features a wide variety of keyboard shortcuts you can use. These will work in bash on any operating system. Some of them may not work if you’re accessing bash remotely through an SSH or telnet session, depending on how you have your keys mapped.

## Working With Processes

* `Ctrl+C`: Interrupt (kill) the current foreground process running-in in the terminal. This sends the `SIGINT` signal to the process, which is technically just a request—most processes will honour it, but some may ignore it.
    
* `Ctrl+Z`: Suspend the current foreground process running in bash. This sends the SIGTSTP signal to the process. To return the process to the foreground later, use the `fg process_name` command.
    
* `Ctrl+D`: Close the bash shell. This sends an EOF (End-of-file) marker to bash, and bash exits when it receives this marker. This is similar to running the `exit` command.
    

## Controlling the Screen

* `Ctrl+L`: Clear the screen. This is similar to running the `clear` command.
    
* `Ctrl+S`: Stop all output to the screen. This is particularly useful when running commands with a lot of long, verbose output, but you don’t want to stop the command itself with `Ctrl+C`.
    
* `Ctrl+Q`: Resume output to the screen after stopping it with `Ctrl+S`.
    

## **Tab Completion**

Tab completion is a very useful bash feature. While typing a file, directory, or command name, press `tab` and bash will automatically complete what you’re typing, if possible. If not, bash will show you various possible matches and you can continue typing and pressing `tab` to finish typing.

## **Working With Your Command History**

* `Up Arrow`: Go to the previous command in the command history.
    
* `Down Arrow`: Go to the next command in the command history.
    
* `Alt+R`: Revert any changes to a command you’ve pulled from your history if you’ve edited it.
    
* `Ctrl+R`: Recall the last command matching the characters you provide. Press this shortcut and start typing to search your bash history for a command.
    
* `Ctrl+O`: Run a command you found with `Ctrl+R`.
    
* `Ctrl+G`: Leave history searching mode without running a command.
    

# The **Shebang**

It is also called `sharp-exclamation`, `sha-bang`, `hashbang`, `pound-bang`, or `hash-pling`.

The shebang line is a character sequence consisting of the characters' number sign and exclamation mark `#!` at the beginning of a script. When a text file with a shebang is used as if it is executable in a Unix-like operating system, the program loader mechanism parses the rest of the file’s initial line as an interpreter directive. The loader executes the specified interpreter program, passing to it as an argument the path that was initially used when attempting to run the script, so that the program may use the file as input data.

The shebang line is usually ignored by the interpreter because the “#” character is a comment marker in many scripting languages; some language interpreters that do not use the hash mark to begin comments still may ignore the shebang line in recognition of its purpose.

```bash
#!/interpreter/[optional-arg]
```

### **Examples:**

* `#!/bin/sh` – Execute the file using the [Bourne shell](https://en.wikipedia.org/wiki/Bourne_shell), or a compatible shell, assumed to be in the `/bin` directory
    
* `#!/bin/bash` – Execute the file using the [Bash shell](https://en.wikipedia.org/wiki/Bash_shell)
    
* `#!/usr/bin/pwsh` – Execute the file using [PowerShell](https://en.wikipedia.org/wiki/PowerShell)
    
* `#!/usr/bin/env python3` – Execute with a [Python](https://en.wikipedia.org/wiki/Python_(programming_language)) interpreter, using the [`env`](https://en.wikipedia.org/wiki/Env) program search path to find it
    
* `#!/bin/false` – Do nothing, but return a non-zero [exit status](https://en.wikipedia.org/wiki/Exit_status), indicating failure. Used to prevent stand-alone execution of a script file intended for execution in a specific context, such as by the `.` command from `sh/bash`, `source` from `csh/tcsh`, or as a `.profile`, `.cshrc`, or `.login` file.
    

# Looking Around

### `ls` (list files and directories)

The `ls` command is used to list the contents of a directory. It is probably the most commonly used Linux command.

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Command</strong></p></td><td colspan="1" rowspan="1"><p><strong>Result</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>ls</code></p></td><td colspan="1" rowspan="1"><p>List the files in the working directory</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>ls /bin</code></p></td><td colspan="1" rowspan="1"><p>List the files in the&nbsp;<code>/bin</code>&nbsp;directory (or any other directory we care to specify)</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>ls -l</code></p></td><td colspan="1" rowspan="1"><p>List the files in the working directory in long format</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>ls -l /etc /bin</code></p></td><td colspan="1" rowspan="1"><p>List the files in the&nbsp;<code>/bin</code>&nbsp;directory and the&nbsp;<code>/etc</code>&nbsp;directory in long format</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>ls -la ..</code></p></td><td colspan="1" rowspan="1"><p>List all files (even ones with names beginning with a period character, which are normally hidden) in the parent of the working directory in a long format</p></td></tr></tbody></table>

A closer look at long format if we use the `-l` option with `ls`

```plaintext


-rw-------     1 me     me       576      Apr 17  2019 weather.txt
drwxr-xr-x     6 me     me       1024     Oct  9  2019 web_page
-rw-rw-r--     1 me     me       276480   Feb 11 20:41 web_site.tar
-rw-------     1 me     me       5743     Dec 16  2018 xmas_file.txt

----------     -------  -------  -------- ------------ -------------
    |             |        |         |         |             |
    |             |        |         |         |         File Name
    |             |        |         |         |
    |             |        |         |         +---  Modification Time
    |             |        |         |
    |             |        |         +-------------   Size (in bytes)
    |             |        |
    |             |        +-----------------------        Group
    |             |
    |             +--------------------------------        Owner
    |
    +----------------------------------------------   File Permissions
```

### `less` (view text files)

`less` is a program that lets us view text files. This is very handy since many of the files used to control and configure Linux are human-readable (I prefer to use `cat` command).

```plaintext
less text_file
```

> **What is "text"?**
> 
> To represent information on a computer, a relationship is defined between the information and some numbers, as computers only understand numbers. All data is converted to numeric representation.
> 
> Representation systems vary in complexity, with some being highly intricate (e.g. compressed multimedia files) and others being quite simple. One of the earliest, simplest systems is called ***ASCII*** *text*, which stands for American Standard Code for Information Interchange. It's an encoding scheme that maps keyboard characters to numbers and was first used on Teletype machines.
> 
> Text is a compact mapping of characters to numbers. Linux systems store many files in text format, and numerous Linux tools work with text files. Even Windows systems recognize the importance of this format; NOTEPAD.EXE is an editor for plain ASCII text files.

Once started, `less` will display the text file one page at a time. Here are some commands that `less` will accept:

<table><tbody><tr><td colspan="1" rowspan="1" colwidth="118"><p><strong>Command</strong></p></td><td colspan="1" rowspan="1"><p><strong>Action</strong></p></td></tr><tr><td colspan="1" rowspan="1" colwidth="118"><p>Page Up or b</p></td><td colspan="1" rowspan="1"><p>Scroll back one page</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="118"><p>Page Down or space</p></td><td colspan="1" rowspan="1"><p>Scroll forward one page</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="118"><p>G</p></td><td colspan="1" rowspan="1"><p>Go to the end of the text file</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="118"><p>1G</p></td><td colspan="1" rowspan="1"><p>Go to the beginning of the text file</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="118"><p>/<em>characters</em></p></td><td colspan="1" rowspan="1"><p>Search forward in the text file for an occurrence of the specified&nbsp;<em>characters</em></p></td></tr><tr><td colspan="1" rowspan="1" colwidth="118"><p>n</p></td><td colspan="1" rowspan="1"><p>Repeat the previous search</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="118"><p>h</p></td><td colspan="1" rowspan="1"><p>Display a complete list <code>less</code> commands and options</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="118"><p>q</p></td><td colspan="1" rowspan="1"><p>Quit</p></td></tr></tbody></table>

### `file` (classify a file's contents)

To efficiently view files in Linux, we can use the `file` command to determine their type.

```bash
file name_of_file
```

Its output looks something like this:

```plaintext
index.html: HTML document, ASCII text
----------  -------------------------
     |                  |              
 File Name          File Type
```

# **A Guided Tour**

The table below lists some interesting places to explore.

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Directory</strong></p></td><td colspan="1" rowspan="1"><p><strong>Description</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/</code></p></td><td colspan="1" rowspan="1"><p>The root directory where the file system begins. The root directory will probably contain only subdirectories.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/boot</code></p></td><td colspan="1" rowspan="1"><p>This is where the Linux kernel and boot loader files are kept. The kernel is a file called&nbsp;<code>vmlinuz</code>.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/etc</code></p></td><td colspan="1" rowspan="1"><p>The&nbsp;<code>/etc</code>&nbsp;directory contains the configuration files for the system. All of the files in&nbsp;<code>/etc</code>&nbsp;should be text files. Some points of interest are:<code>/etc/passwd</code>The&nbsp;<code>passwd</code>&nbsp;file contains the essential information for each user. This is where user accounts are defined.<code>/etc/fstab</code>The&nbsp;<code>fstab</code>&nbsp;file contains a table of devices that get mounted when the system boots. This file defines the system's disk drives.<code>/etc/hosts</code>This file lists the network host names and IP addresses that are intrinsically known to the system.<code>/etc/init.d</code>This directory contains the scripts that start various system services at boot time.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/bin, /usr/bin</code></p></td><td colspan="1" rowspan="1"><p>These two directories contain most of the programs for the system. The&nbsp;<code>/bin</code>&nbsp;directory has the essential programs that the system requires to operate, while&nbsp;<code>/usr/bin</code>&nbsp;contains applications for the system's users.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/sbin, /usr/sbin</code></p></td><td colspan="1" rowspan="1"><p>The&nbsp;<code>sbin</code>&nbsp;directories contain programs for system administration, mostly for use by the superuser.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/usr</code></p></td><td colspan="1" rowspan="1"><p>The&nbsp;<code>/usr</code>&nbsp;directory contains a variety of things that support user applications. Some highlights:<code>/usr/share/X11</code>Support files for the X Window system<code>/usr/share/dict</code>Dictionaries for the spelling checker. Yes, Linux comes with a spelling checker. See&nbsp;<a target="_blank" rel="noopener noreferrer nofollow" href="http://linuxcommand.org/lc3_man_pages/look1.html" style="pointer-events: none"><code>look</code></a>&nbsp;and&nbsp;<a target="_blank" rel="noopener noreferrer nofollow" href="http://linuxcommand.org/lc3_man_pages/aspell1.html" style="pointer-events: none"><code>aspell</code></a>.<code>/usr/share/doc</code>Various documentation files in a variety of formats.<code>/usr/share/man</code>The man pages are kept here.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/usr/local</code></p></td><td colspan="1" rowspan="1"><p><code>/usr/local</code>&nbsp;and its subdirectories are used for the installation of software and other files for use on the local machine. What this really means is that software that is not part of the official distribution (which usually goes in&nbsp;<code>/usr/bin</code>) goes here. When you find interesting programs to install on your system, they should be installed in one of the&nbsp;<code>/usr/local</code>&nbsp;directories. Most often, the directory of choice is&nbsp;<code>/usr/local/bin</code>.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/var</code></p></td><td colspan="1" rowspan="1"><p>The&nbsp;<code>/var</code>&nbsp;directory contains files that change as the system is running. This includes:<code>/var/log</code>Directory that contains log files. These are updated as the system runs. It's a good idea to view the files in this directory from time to time, to monitor the health of your system.<code>/var/spool</code>This directory is used to hold files that are queued for some process, such as mail messages and print jobs. When a user's mail first arrives on the local system (assuming it has local mail, a rare occurrence on modern machines that are not mail servers), the messages are first stored in&nbsp;<code>/var/spool/mail</code></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/lib</code></p></td><td colspan="1" rowspan="1"><p>The shared libraries (similar to DLLs in that other operating system) are kept here.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/home</code></p></td><td colspan="1" rowspan="1"><p><code>/home</code>&nbsp;is where users keep their personal work. In general, this is the only place users are allowed to write files. This keeps things nice and clean :-)</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/root</code></p></td><td colspan="1" rowspan="1"><p>This is the superuser's home directory.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/tmp</code></p></td><td colspan="1" rowspan="1"><p><code>/tmp</code>&nbsp;is a directory in which programs can write their temporary files.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/dev</code></p></td><td colspan="1" rowspan="1"><p>The&nbsp;<code>/dev</code>&nbsp;directory is a special directory, since it does not really contain files in the usual sense. Rather, it contains devices that are available to the system. In Linux (like Unix), devices are treated like files. You can read and write devices as though they were files. For example&nbsp;<code>/dev/fd0</code>&nbsp;is the first floppy disk drive,&nbsp;<code>/dev/sda</code>&nbsp;is the first hard drive. All the devices that the kernel understands are represented here.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/proc</code></p></td><td colspan="1" rowspan="1"><p>The&nbsp;<code>/proc</code>&nbsp;directory is also special. This directory does not contain files. In fact, this directory does not really exist at all. It is entirely virtual. The&nbsp;<code>/proc</code>&nbsp;directory contains little peep holes into the kernel itself. There are a group of numbered entries in this directory that correspond to all the processes running on the system. In addition, there are a number of named entries that permit access to the current configuration of the system. Many of these entries can be viewed. Try viewing&nbsp;<code>/proc/cpuinfo</code>. This entry will tell you what the kernel thinks of the system's CPU.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>/media</code></p></td><td colspan="1" rowspan="1"><p>Finally, we come to&nbsp;<code>/media</code>, a normal directory which is used in a special way. The&nbsp;<code>/media</code>&nbsp;directory is used for&nbsp;<em>mount points</em>. As we learned in the&nbsp;<a target="_blank" rel="noopener noreferrer nofollow" href="http://linuxcommand.org/lc3_lts0020.php" style="pointer-events: none">second lesson</a>, the different physical storage devices (like hard disk drives) are attached to the file system tree in various places. This process of attaching a device to the tree is called&nbsp;<em>mounting</em>. For a device to be available, it must first be mounted. When your system boots, it reads a list of mounting instructions in the&nbsp;<code>/etc/fstab</code>&nbsp;file, which describes which device is mounted at which mount point in the directory tree. This takes care of the hard drives, but we may also have devices that are considered temporary, such as optical disks and USB storage devices. Since these are removable, they do not stay mounted all the time. The&nbsp;<code>/media</code>&nbsp;directory is used by the automatic device mounting mechanisms found in modern desktop oriented Linux distributions. To see what devices and mount points are used, type&nbsp;<a target="_blank" rel="noopener noreferrer nofollow" href="http://linuxcommand.org/lc3_man_pages/mount8.html" style="pointer-events: none"><code>mount</code></a>.</p></td></tr></tbody></table>

> A weird kind of file...
> 
> During your tour, you probably noticed a strange kind of directory entry, particularly in the /lib directory. When listed with ls -l, you might have seen something like this:
> 
> ```bash
> lrwxrwxrwx     25 Jul  3 16:42 System.map -> /boot/System.map-4.0.36-3
> -rw-r--r-- 105911 Oct 13  2018 System.map-4.0.36-0.7
> -rw-r--r-- 105935 Dec 29  2018 System.map-4.0.36-3
> -rw-r--r-- 181986 Dec 11  2019 initrd-4.0.36-0.7.img
> -rw-r--r-- 182001 Dec 11  2019 initrd-4.0.36.img
> lrwxrwxrwx   26 Jul  3 16:42 module-info -> /boot/module-info-4.0.36-3
> -rw-r--r--  11773 Oct 13  2018 module-info-4.0.36-0.7
> -rw-r--r--  11773 Dec 29  2018 module-info-4.0.36-3
> lrwxrwxrwx     16 Dec 11  2019 vmlinuz -> vmlinuz-4.0.36-3
> -rw-r--r-- 454325 Oct 13  2018 vmlinuz-4.0.36-0.7
> -rw-r--r-- 454434 Dec 29  2018 vmlinuz-4.0.36-3
> ```
> 
> Notice the files, [`system.map`](http://System.map)`, module-info` and `vmlinuz`. See the strange notation after the file names?
> 
> Files such as this are called symbolic links. Symbolic links are a special type of file that points to another file. With symbolic links, it is possible for a single file to have multiple names. Here's how it works: Whenever the system is given a file name that is a symbolic link, it transparently maps it to the file it is pointing to.
> 
> Just what is this good for? This is a very handy feature. Let's consider the directory listing above (which is the `/boot` directory of an old system). This system has had multiple versions of the Linux kernel installed. We can see this from the files `vmlinuz-4.0.36-0.7` and `vmlinuz-4.0.36-3`. These file names suggest that both version 4.0.36-0.7 and 4.0.36-3 are installed. Because the file names contain the version it is easy to see the differences in the directory listing. However, this would be confusing to programs that rely on a fixed name for the kernel file. These programs might expect the kernel to simply be called `vmlinuz`. Here is where the beauty of the symbolic link comes in. By creating a symbolic link called `vmlinuz` that points to `vmlinuz-4.0.36-3`, we have solved the problem.
> 
> To create symbolic links, we use the [`ln`](http://linuxcommand.org/lc3_man_pages/ln1.html) command.

# **Manipulating Files**

Now, to be frank, some of the tasks performed by these commands are more easily done with a graphical file manager. With a file manager, you can drag and drop a file from one directory to another, cut and paste files, delete files, etc. So why use these old command line programs?

Then, how would you copy all the HTML files from one directory to another, but only copy files that did not exist in the destination directory or were newer than the versions in the destination directory? Pretty hard with a file manager. Pretty easy with the command line:

```bash
[me@linuxbox me]$ cp -u *.html destination
```

## **Wildcards**

Before we start using commands, let's learn about a shell feature that makes them powerful - wildcards. These special characters allow you to select filenames based on patterns of characters. See the table below for the list of wildcards and what they select:

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Wildcard</strong></p></td><td colspan="1" rowspan="1"><p><strong>Meaning</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>*</code></p></td><td colspan="1" rowspan="1"><p>Matches any characters</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>?</code></p></td><td colspan="1" rowspan="1"><p>Matches any single character</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>[characters]</code></p></td><td colspan="1" rowspan="1"><p>Matches any character that is a member of the set&nbsp;<em>characters</em>. The set of characters may also be expressed as a&nbsp;<em>POSIX character class</em>&nbsp;such as one of the following:<br><code>[:alnum:]</code><strong> </strong>Alphanumeric characters.<br><code>[:alpha:]</code><strong> </strong>Alphabetic characters.<br><code>[:digit:]</code><strong> </strong>Numerals.<br><code>[:upper:]</code><strong> </strong>Uppercase alphabetic characters.<br><code>[:lower:]</code><strong> </strong>Lowercase alphabetic characters.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>[!characters]</code></p></td><td colspan="1" rowspan="1"><p>Matches any character that is not a member of the set&nbsp;<em>characters</em></p></td></tr></tbody></table>

Here are some examples of patterns and what they match:

<table><tbody><tr><td colspan="1" rowspan="1" colwidth="260"><p><strong>Pattern</strong></p></td><td colspan="1" rowspan="1"><p><strong>Matches</strong></p></td></tr><tr><td colspan="1" rowspan="1" colwidth="260"><p><code>*</code></p></td><td colspan="1" rowspan="1"><p>All filenames</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="260"><p><code>g*</code></p></td><td colspan="1" rowspan="1"><p>All filenames that begin with the character "g"</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="260"><p><code>b*.txt</code></p></td><td colspan="1" rowspan="1"><p>All filenames that begin with the character "b" and end with the characters ".txt"</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="260"><p><code>Data???</code></p></td><td colspan="1" rowspan="1"><p>Any filename that begins with the characters "Data" followed by exactly 3 more characters</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="260"><p><code>[abc]*</code></p></td><td colspan="1" rowspan="1"><p>Any filename that begins with "a" or "b" or "c" followed by any other characters</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="260"><p><code>[[:upper:]]*</code></p></td><td colspan="1" rowspan="1"><p>Any filename that begins with an uppercase letter. This is an example of a character class.</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="260"><p><code>BACKUP.[[:digit:]][[:digit:]]</code></p></td><td colspan="1" rowspan="1"><p>Another example of character classes. This pattern matches any filename that begins with the characters "BACKUP." followed by exactly two numerals.</p></td></tr><tr><td colspan="1" rowspan="1" colwidth="260"><p><code>*[![:lower:]]</code></p></td><td colspan="1" rowspan="1"><p>Any filename that does not end with a lowercase letter.</p></td></tr></tbody></table>

> We can use wildcards with any command that accepts filename arguments.
> 
> A note on notation: `...` signifies that an item can be repeated one or more times.

These four commands are among the most frequently used Linux commands. They are the basic commands for manipulating both files and directories:

### `cp` (copy files and directories)

The `cp` program copies files and directories.

```bash
[me@linuxbox me]$ cp file1 file2
```

Other useful examples of `cp` and its options include:

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Command</strong></p></td><td colspan="1" rowspan="1"><p><strong>Results</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>cp&nbsp;file1 file2</code></p></td><td colspan="1" rowspan="1"><p>Copies the contents of&nbsp;<em>file1</em>&nbsp;into&nbsp;<em>file2</em>. If&nbsp;<em>file2</em>&nbsp;does not exist, it is created;&nbsp;<strong>otherwise,&nbsp;<em>file2</em>&nbsp;is silently overwritten with the contents of&nbsp;<em>file1</em>.</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>cp -i&nbsp;file1 file2</code></p></td><td colspan="1" rowspan="1"><p>Like above however, since the <code>-i</code> (interactive) option is specified, if&nbsp;<em>file2</em>&nbsp;exists, the user is prompted before it is overwritten with the contents of&nbsp;<em>file1</em>.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>cp&nbsp;file1 dir1</code></p></td><td colspan="1" rowspan="1"><p>Copy the contents of&nbsp;<em>file1</em>&nbsp;(into a file named&nbsp;<em>file1</em>) inside of directory&nbsp;<em>dir1</em>.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>cp -R&nbsp;dir1 dir2</code></p></td><td colspan="1" rowspan="1"><p>Copy the contents of the directory&nbsp;<em>dir1</em>. If directory&nbsp;<em>dir2</em>&nbsp;does not exist, it is created. Otherwise, it creates a directory named&nbsp;<em>dir1</em>&nbsp;within directory&nbsp;<em>dir2</em>.</p></td></tr></tbody></table>

### `mv` (move or rename files and directories)

The `mv` command moves or renames files and directories depending on how it is used. It will either move one or more files to a different directory, or it will rename a file or directory. To rename a file.

```bash
[me@linuxbox me]$ mv filename1 filename2
```

Examples of `mv` and its options include:

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Command</strong></p></td><td colspan="1" rowspan="1"><p><strong>Results</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>mv&nbsp;file1 file2</code></p></td><td colspan="1" rowspan="1"><p>If&nbsp;<em>file2</em>&nbsp;does not exist, then&nbsp;<em>file1</em>&nbsp;is renamed&nbsp;<em>file2</em>.&nbsp;<strong>If&nbsp;<em>file2</em>&nbsp;exists, its contents are silently replaced with the contents of&nbsp;<em>file1</em>.</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>mv -i&nbsp;file1 file2</code></p></td><td colspan="1" rowspan="1"><p>Like above however, since the <code>-i</code> (interactive) option is specified, if&nbsp;<em>file2</em>&nbsp;exists, the user is prompted before it is overwritten with the contents of&nbsp;<em>file1</em>.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>mv&nbsp;file1 file2 dir1</code></p></td><td colspan="1" rowspan="1"><p>The files&nbsp;<em>file1</em>&nbsp;and&nbsp;<em>file2&nbsp;</em>are moved to directory&nbsp;<em>dir1</em>. If&nbsp;<em>dir1</em>&nbsp;does not exist,&nbsp;<code>mv</code>&nbsp;will exit with an error.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>mv&nbsp;dir1 dir2</code></p></td><td colspan="1" rowspan="1"><p>If&nbsp;<em>dir2</em>&nbsp;does not exist, then&nbsp;<em>dir1</em>&nbsp;is renamed&nbsp;<em>dir2</em>. If&nbsp;<em>dir2</em>&nbsp;exists, the directory&nbsp;<em>dir1</em>&nbsp;is moved within directory&nbsp;<em>dir2</em>.</p></td></tr></tbody></table>

### `rm` (remove files and directories)

The `rm` command removes (deletes) files and directories.

```bash
[me@linuxbox me]$ rm file...
```

Using the recursive option `-r`, `rm` can also be used to delete directories:

```bash
[me@linuxbox me]$ rm -r directory...
```

Examples of `rm` and its options include:

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Command</strong></p></td><td colspan="1" rowspan="1"><p><strong>Results</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>rm&nbsp;file1 file2</code></p></td><td colspan="1" rowspan="1"><p>Delete&nbsp;<em>file1</em>&nbsp;and&nbsp;<em>file2</em>.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>rm -i&nbsp;file1 file2</code></p></td><td colspan="1" rowspan="1"><p>Like above however, since the <code>-i</code> (interactive) option is specified, the user is prompted before each file is deleted.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>rm -r&nbsp;dir1 dir2</code></p></td><td colspan="1" rowspan="1"><p>Directories&nbsp;<em>dir1</em>&nbsp;and&nbsp;<em>dir2</em>&nbsp;are deleted along with all of their contents.</p></td></tr></tbody></table>

> `rm` **IS DANGROUS!**
> 
> Linux does not have an undelete command. Once you delete something with `rm`, it's gone. You can inflict terrific damage on your system with `rm` if you are not careful, particularly with wildcards.
> 
> Try construct your command using `ls` instead. By doing this, you can see the effect of your wildcards before you delete files.

### `mkdir` (create directories)

The `mkdir` command is used to create directories.

```bash
[me@linuxbox me]$ mkdir directory...
```

Since the commands we have covered here accept multiple file and directories names as arguments, you can use wildcards to specify them. Here are a few examples:

<table><tbody><tr><td colspan="1" rowspan="1"><p><strong>Command</strong></p></td><td colspan="1" rowspan="1"><p><strong>Results</strong></p></td></tr><tr><td colspan="1" rowspan="1"><p><code>cp *.txt text_files</code></p></td><td colspan="1" rowspan="1"><p>Copy all files in the current working directory with names ending with the characters ".txt" to an existing directory named&nbsp;<em>text_files</em>.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>mv dir1 ../*.bak dir2</code></p></td><td colspan="1" rowspan="1"><p>Move the subdirectory&nbsp;<em>dir1</em>&nbsp;and all the files ending in <code>.bak</code> in the current working directory's parent directory to an existing directory named&nbsp;<em>dir2</em>.</p></td></tr><tr><td colspan="1" rowspan="1"><p><code>rm *~</code></p></td><td colspan="1" rowspan="1"><p>Delete all files in the current working directory that end with the character "~". Some applications create backup files using this naming scheme. Using this command will clean them out of a directory.</p></td></tr></tbody></table>

> [Buy me a coffee](https://linktr.ee/joehsn) ☕ to help me keep going, thanks in advance! ❤

# Resources

* [What Is “The Shell”?](https://intranet.alxswe.com/rltoken/vwO91sqNBgRL03BLu-ueiA)
    
* [What are the Different Types of Shells in Linux?](https://www.digitalocean.com/community/tutorials/different-types-of-shells-in-linux)
    
* [Navigation](https://intranet.alxswe.com/rltoken/iblidp7yp6i-QpT8rDXHaA)
    
* [Looking Around](https://intranet.alxswe.com/rltoken/xEKUCnQsMH0esQ6fJU5vLA)
    
* [A Guided Tour](https://intranet.alxswe.com/rltoken/HUhQ73fFR1GOC5nb4r-mDw)
    
* [Manipulating Files](https://intranet.alxswe.com/rltoken/olv-1tj4d1LA57Z0PrLNvw)
    
* [Working With Commands](https://intranet.alxswe.com/rltoken/zUtux3Pm0BkvtwXzbTtkmA)
    
* [Keyboard shortcuts for Bash](https://intranet.alxswe.com/rltoken/AGxMxuS5IeW8VmEvJyhwvw)
    
* [Shebang](https://intranet.alxswe.com/rltoken/cE8ZA3kgEaFhB-IDNv31bQ)