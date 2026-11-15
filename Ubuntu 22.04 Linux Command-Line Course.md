# Ubuntu 22.04 Linux Command-Line Course
## University Computer Science Edition
### Beginner → Intermediate → Advanced → System Administration → Bash → Networking → Security

> **Purpose**
>
> This document is a comprehensive Linux command-line teaching reference for university computer science students using **Ubuntu 22.04 LTS**.
>
> It intentionally focuses on **general Linux and computer science skills**. It does not depend on robotics, ROS, or any particular application domain.
>
> **Important:** Linux has thousands of commands and utilities. No single course can literally list every command installed on every Ubuntu system. This course covers the major commands, command families, shell concepts, administration tools, networking tools, development utilities, and troubleshooting techniques that CS students should know.

---

# Table of Contents

1. [Linux Fundamentals](#1-linux-fundamentals)
2. [Opening and Understanding the Terminal](#2-opening-and-understanding-the-terminal)
3. [Command Structure](#3-command-structure)
4. [Getting Help](#4-getting-help)
5. [Filesystem Hierarchy](#5-filesystem-hierarchy)
6. [Navigation Commands](#6-navigation-commands)
7. [Listing Files](#7-listing-files)
8. [Creating Files and Directories](#8-creating-files-and-directories)
9. [Copying, Moving, and Renaming](#9-copying-moving-and-renaming)
10. [Deleting Files](#10-deleting-files)
11. [File Types](#11-file-types)
12. [Reading Files](#12-reading-files)
13. [Text Editors](#13-text-editors)
14. [Wildcards and Pattern Matching](#14-wildcards-and-pattern-matching)
15. [Quoting and Escaping](#15-quoting-and-escaping)
16. [Pipes](#16-pipes)
17. [Input and Output Redirection](#17-input-and-output-redirection)
18. [Command Chaining](#18-command-chaining)
19. [Exit Status](#19-exit-status)
20. [Environment Variables](#20-environment-variables)
21. [PATH](#21-path)
22. [Aliases and Shell Functions](#22-aliases-and-shell-functions)
23. [Users and Groups](#23-users-and-groups)
24. [File Ownership](#24-file-ownership)
25. [File Permissions](#25-file-permissions)
26. [Advanced Permissions](#26-advanced-permissions)
27. [sudo and Root](#27-sudo-and-root)
28. [Finding Files](#28-finding-files)
29. [Searching File Contents](#29-searching-file-contents)
30. [sort, uniq, wc, cut, tr](#30-sort-uniq-wc-cut-tr)
31. [awk](#31-awk)
32. [sed](#32-sed)
33. [Regular Expressions](#33-regular-expressions)
34. [xargs](#34-xargs)
35. [Processes](#35-processes)
36. [Signals](#36-signals)
37. [Foreground and Background Jobs](#37-foreground-and-background-jobs)
38. [Process Priority](#38-process-priority)
39. [System Monitoring](#39-system-monitoring)
40. [The /proc Filesystem](#40-the-proc-filesystem)
41. [The /sys Filesystem](#41-the-sys-filesystem)
42. [Disk Space](#42-disk-space)
43. [Block Devices](#43-block-devices)
44. [Mounting Filesystems](#44-mounting-filesystems)
45. [Archives and Compression](#45-archives-and-compression)
46. [Package Management with APT](#46-package-management-with-apt)
47. [dpkg](#47-dpkg)
48. [System Services and systemd](#48-system-services-and-systemd)
49. [System Logs](#49-system-logs)
50. [Networking Fundamentals](#50-networking-fundamentals)
51. [Network Interfaces](#51-network-interfaces)
52. [DNS](#52-dns)
53. [Ports and Sockets](#53-ports-and-sockets)
54. [SSH](#54-ssh)
55. [Secure File Transfer](#55-secure-file-transfer)
56. [curl and wget](#56-curl-and-wget)
57. [Network Diagnostics](#57-network-diagnostics)
58. [Bash Scripting](#58-bash-scripting)
59. [Shell Variables](#59-shell-variables)
60. [Script Arguments](#60-script-arguments)
61. [Conditions](#61-conditions)
62. [Loops](#62-loops)
63. [Functions](#63-functions)
64. [Arrays](#64-arrays)
65. [Command Substitution](#65-command-substitution)
66. [Arithmetic](#66-arithmetic)
67. [Shell Input](#67-shell-input)
68. [Signals and Traps in Scripts](#68-signals-and-traps-in-scripts)
69. [Debugging Bash Scripts](#69-debugging-bash-scripts)
70. [Cron and Scheduled Tasks](#70-cron-and-scheduled-tasks)
71. [System Information](#71-system-information)
72. [Time and Date](#72-time-and-date)
73. [Users, Sessions, and Login Information](#73-users-sessions-and-login-information)
74. [Process and Resource Limits](#74-process-and-resource-limits)
75. [Shared Libraries](#75-shared-libraries)
76. [Compilers and Build Tools](#76-compilers-and-build-tools)
77. [Environment and Development Tools](#77-environment-and-development-tools)
78. [Git](#78-git)
79. [Checksums and File Integrity](#79-checksums-and-file-integrity)
80. [Encryption Basics](#80-encryption-basics)
81. [Permissions and Security Diagnostics](#81-permissions-and-security-diagnostics)
82. [Symbolic Links and Hard Links](#82-symbolic-links-and-hard-links)
83. [File Descriptors](#83-file-descriptors)
84. [Named Pipes and IPC](#84-named-pipes-and-ipc)
85. [Terminal Control](#85-terminal-control)
86. [tmux](#86-tmux)
87. [Common Command-Line Utilities](#87-common-command-line-utilities)
88. [Advanced Command Combinations](#88-advanced-command-combinations)
89. [Linux Troubleshooting Method](#89-linux-troubleshooting-method)
90. [Essential Command Cheat Sheet](#90-essential-command-cheat-sheet)
91. [University Practice Exercises](#91-university-practice-exercises)
92. [Suggested Semester Progression](#92-suggested-semester-progression)

---

# 1. Linux Fundamentals

Linux is an operating system kernel. Ubuntu is a Linux distribution that combines:

```text
Linux kernel
+
GNU utilities
+
system libraries
+
package management
+
desktop/server software
+
configuration
```

A Linux system can be used through:

```text
GUI
CLI / Terminal
SSH
Scripts
Programs
System APIs
```

This course focuses on the **CLI (Command-Line Interface)**.

---

# 2. Opening and Understanding the Terminal

Open Terminal:

```text
Ctrl + Alt + T
```

A typical shell prompt may look like:

```text
student@ubuntu:~$
```

Breakdown:

```text
student     current username
@           separator
ubuntu      hostname
:           separator
~           current directory
$           normal user
```

Root often uses:

```text
#
```

---

## Essential first commands

```bash
pwd
```

Print current working directory.

```bash
whoami
```

Print current username.

```bash
hostname
```

Print computer hostname.

```bash
date
```

Print date and time.

```bash
clear
```

Clear terminal screen.

```bash
history
```

Show command history.

---

# 3. Command Structure

Most commands follow:

```text
command [options] [arguments]
```

Example:

```bash
ls -lah /home/student
```

Here:

```text
ls                  command
-l -a -h            options
/home/student       argument
```

Options can often be combined:

```bash
ls -l -a -h
```

becomes:

```bash
ls -lah
```

Long options commonly use:

```bash
ls --all --human-readable
```

---

# 4. Getting Help

Linux provides several ways to learn commands.

## `--help`

```bash
ls --help
```

Short version:

```bash
ls -h
```

Note: `-h` does not always mean help. Options depend on the command.

---

## `man`

```bash
man ls
```

Manual pages are one of the most important Linux learning resources.

Useful keys:

```text
Space       next page
b           previous page
/word       search
n           next search result
q           quit
```

---

## `info`

Some GNU utilities have detailed documentation:

```bash
info coreutils
```

---

## `whatis`

```bash
whatis ls
```

---

## `apropos`

Search manual descriptions:

```bash
apropos network
```

Equivalent style:

```bash
man -k network
```

---

## `type`

Determine what a command actually is:

```bash
type cd
type ls
type python3
```

It can reveal:

```text
shell builtin
alias
function
external command
```

---

## `which`

Find an executable:

```bash
which python3
```

---

## `whereis`

Find related program files:

```bash
whereis python3
```

---

# 5. Filesystem Hierarchy

Linux has one tree beginning at:

```text
/
```

Important directories:

```text
/
├── bin       Essential user commands
├── boot      Boot files
├── dev       Device files
├── etc       System configuration
├── home      User home directories
├── lib       Essential libraries
├── media     Removable media
├── mnt       Temporary mount points
├── opt       Optional software
├── proc      Process/kernel virtual filesystem
├── root      Root user's home
├── run       Runtime system data
├── sbin      System administration commands
├── srv       Service data
├── sys       Kernel/device virtual filesystem
├── tmp       Temporary files
├── usr       Most user applications/libraries
└── var       Variable data, logs, caches
```

Modern Ubuntu systems may use merged `/usr` layouts, so some traditional directories can be symbolic links.

---

# 6. Navigation Commands

## `pwd`

```bash
pwd
```

Example:

```text
/home/student
```

---

## `cd`

```bash
cd Documents
```

Go home:

```bash
cd ~
```

Go to root:

```bash
cd /
```

Go up:

```bash
cd ..
```

Go up two levels:

```bash
cd ../..
```

Return to previous directory:

```bash
cd -
```

---

## Special path symbols

```text
/       filesystem root
.       current directory
..      parent directory
~       current user's home
```

---

# 7. Listing Files

## Basic

```bash
ls
```

Long listing:

```bash
ls -l
```

Hidden files:

```bash
ls -a
```

Human-readable:

```bash
ls -h
```

Combine:

```bash
ls -lah
```

Sort by modification time:

```bash
ls -lt
```

Reverse order:

```bash
ls -ltr
```

Directories only:

```bash
ls -ld */
```

Recursive listing:

```bash
ls -R
```

---

# 8. Creating Files and Directories

## `mkdir`

```bash
mkdir project
```

Nested directories:

```bash
mkdir -p project/src/main
```

---

## `touch`

```bash
touch file.txt
```

Multiple:

```bash
touch a.txt b.txt c.txt
```

`touch` creates a file if it does not exist.

If it exists, it updates timestamps by default.

---

# 9. Copying, Moving, and Renaming

## `cp`

```bash
cp source.txt destination.txt
```

Copy into directory:

```bash
cp source.txt Documents/
```

Recursive directory copy:

```bash
cp -r project project_backup
```

Preserve attributes:

```bash
cp -a project project_backup
```

---

## `mv`

Move:

```bash
mv file.txt Documents/
```

Rename:

```bash
mv old.txt new.txt
```

Move and rename:

```bash
mv old.txt Documents/new.txt
```

---

# 10. Deleting Files

Delete file:

```bash
rm file.txt
```

Interactive:

```bash
rm -i file.txt
```

Recursive directory:

```bash
rm -r project/
```

Interactive recursive:

```bash
rm -ri project/
```

Force:

```bash
rm -f file.txt
```

Force recursive:

```bash
rm -rf project/
```

## Safety rule

Never run destructive commands without understanding:

```bash
pwd
ls
```

Be especially careful with:

```bash
sudo rm -rf ...
```

Linux command-line deletion usually bypasses the desktop Trash.

---

# 11. File Types

Use:

```bash
file filename
```

Examples:

```bash
file image.png
file program
file archive.tar.gz
```

Common file types include:

```text
regular file
directory
symbolic link
block device
character device
socket
FIFO
```

---

## `stat`

Detailed file information:

```bash
stat file.txt
```

Shows:

```text
size
permissions
owner
group
timestamps
inode
```

---

# 12. Reading Files

## `cat`

```bash
cat file.txt
```

Number lines:

```bash
cat -n file.txt
```

---

## `less`

```bash
less file.txt
```

Useful keys:

```text
Space       next page
b           previous page
g           beginning
G           end
/word       search
n           next match
q           quit
```

---

## `more`

```bash
more file.txt
```

Older/simple pager.

---

## `head`

```bash
head file.txt
```

First 20 lines:

```bash
head -20 file.txt
```

---

## `tail`

```bash
tail file.txt
```

Last 20:

```bash
tail -20 file.txt
```

Follow changes:

```bash
tail -f logfile
```

---

# 13. Text Editors

## nano

```bash
nano file.txt
```

Important shortcuts:

```text
Ctrl+O     save
Ctrl+X     exit
Ctrl+W     search
Ctrl+K     cut line
Ctrl+U     paste
```

---

## vim

```bash
vim file.txt
```

Minimum useful commands:

```text
i       insert
Esc     normal mode
:w      save
:q      quit
:wq     save and quit
:q!     quit without saving
```

---

## emacs

If installed:

```bash
emacs file.txt
```

---

# 14. Wildcards and Pattern Matching

## `*`

Matches zero or more characters.

```bash
ls *.txt
```

Matches:

```text
a.txt
notes.txt
report.txt
```

---

## `?`

Matches exactly one character.

```bash
ls file?.txt
```

---

## Character classes

```bash
ls file[123].txt
```

Matches:

```text
file1.txt
file2.txt
file3.txt
```

Ranges:

```bash
ls file[0-9].txt
```

---

# 15. Quoting and Escaping

Shell metacharacters have special meanings.

Example:

```bash
echo *
```

expands to filenames.

To prevent expansion:

```bash
echo "*"
```

---

## Double quotes

```bash
echo "$HOME"
```

Variables are expanded.

---

## Single quotes

```bash
echo '$HOME'
```

`$HOME` is treated literally.

---

## Escape character

```bash
echo \$HOME
```

Prints:

```text
$HOME
```

---

## Filenames with spaces

Use quotes:

```bash
cd "My Documents"
```

or escape spaces:

```bash
cd My\ Documents
```

---

# 16. Pipes

The pipe operator:

```text
|
```

connects the output of one command to the input of another.

Example:

```bash
ls -lah | less
```

Example:

```bash
ps aux | grep python
```

Example:

```bash
cat file.txt | sort
```

A pipe is conceptually:

```text
Command A
   │
   │ stdout
   ▼
Command B
   │
   │ stdout
   ▼
Command C
```

This is one of the most important Unix design principles:

> Small programs can be combined to perform complex operations.

---

# 17. Input and Output Redirection

Every process normally has:

```text
stdin   0
stdout  1
stderr  2
```

---

## `>`

Write stdout:

```bash
ls > files.txt
```

Existing contents are replaced.

---

## `>>`

Append:

```bash
ls >> files.txt
```

---

## `<`

Read stdin from a file:

```bash
sort < names.txt
```

---

## Redirect stderr

```bash
command 2> errors.txt
```

---

## Redirect stdout and stderr

```bash
command > output.txt 2>&1
```

Common shorthand:

```bash
command &> output.txt
```

---

## Redirect only stdout to `/dev/null`

```bash
command > /dev/null
```

Ignore stderr too:

```bash
command > /dev/null 2>&1
```

`/dev/null` is effectively a data sink.

---

# 18. Command Chaining

## `&&`

Run next command only if previous command succeeds:

```bash
mkdir build && cd build
```

---

## `||`

Run next command only if previous command fails:

```bash
command || echo "Command failed"
```

---

## `;`

Run regardless:

```bash
command1 ; command2
```

---

## Group commands

```bash
(command1; command2)
```

Runs in a subshell.

Current shell grouping:

```bash
{ command1; command2; }
```

---

# 19. Exit Status

Every command returns an exit status.

Convention:

```text
0       success
nonzero error/failure
```

Check previous command:

```bash
echo $?
```

Example:

```bash
true
echo $?
```

Result:

```text
0
```

Try:

```bash
false
echo $?
```

Result:

```text
1
```

This concept is essential for Bash scripting and automation.

---

# 20. Environment Variables

Show all:

```bash
printenv
```

or:

```bash
env
```

Show one:

```bash
echo "$HOME"
```

Common variables:

```text
HOME
PATH
USER
SHELL
PWD
OLDPWD
LANG
TERM
```

Set:

```bash
export MY_VARIABLE="hello"
```

Read:

```bash
echo "$MY_VARIABLE"
```

Unset:

```bash
unset MY_VARIABLE
```

---

# 21. PATH

Show PATH:

```bash
echo "$PATH"
```

Example:

```text
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

When you type:

```bash
python3
```

the shell searches directories in `$PATH`.

Find command:

```bash
which python3
```

More information:

```bash
type python3
```

Add a directory temporarily:

```bash
export PATH="$HOME/bin:$PATH"
```

---

# 22. Aliases and Shell Functions

Create an alias:

```bash
alias ll='ls -lah'
```

Use:

```bash
ll
```

List aliases:

```bash
alias
```

Remove:

```bash
unalias ll
```

Aliases normally disappear when the shell exits unless saved in shell configuration.

---

## Functions

```bash
mkcd() {
    mkdir -p "$1" && cd "$1"
}
```

Then:

```bash
mkcd project
```

Functions are more powerful than aliases because they can accept arguments and perform logic.

---

# 23. Users and Groups

Current user:

```bash
whoami
```

Identity:

```bash
id
```

Groups:

```bash
groups
```

---

## User database

```bash
cat /etc/passwd
```

Password database:

```bash
sudo cat /etc/shadow
```

Do not casually modify `/etc/shadow`.

---

## Add user

```bash
sudo adduser student2
```

---

## Delete user

```bash
sudo deluser student2
```

---

## Add group

```bash
sudo groupadd developers
```

---

## Add user to group

```bash
sudo usermod -aG developers student2
```

The `-a` is important: it appends instead of replacing existing supplementary groups.

---

# 24. File Ownership

Check:

```bash
ls -l
```

Example:

```text
-rw-r--r-- 1 student students 1200 file.txt
```

Here:

```text
student       owner
students      group
```

---

## `chown`

Change owner:

```bash
sudo chown alice file.txt
```

Owner and group:

```bash
sudo chown alice:developers file.txt
```

Recursive:

```bash
sudo chown -R alice:developers project/
```

Use recursive ownership changes carefully.

---

## `chgrp`

Change group:

```bash
sudo chgrp developers file.txt
```

---

# 25. File Permissions

Example:

```text
-rwxr-xr--
```

Breakdown:

```text
owner    rwx
group    r-x
others   r--
```

Permissions:

```text
r = read
w = write
x = execute
```

---

## Symbolic chmod

Add execute:

```bash
chmod +x script.sh
```

Owner write:

```bash
chmod u+w file.txt
```

Group write:

```bash
chmod g+w file.txt
```

Others write:

```bash
chmod o+w file.txt
```

Remove:

```bash
chmod o-w file.txt
```

---

## Numeric chmod

Values:

```text
r = 4
w = 2
x = 1
```

Therefore:

```text
rwx = 7
rw- = 6
r-x = 5
r-- = 4
```

Example:

```bash
chmod 755 script.sh
```

Means:

```text
owner  = 7 = rwx
group  = 5 = r-x
others = 5 = r-x
```

Private file:

```bash
chmod 600 private.txt
```

---

# 26. Advanced Permissions

## Setuid

```text
s
```

Setuid causes an executable to run with the file owner's effective identity.

View:

```bash
ls -l /usr/bin/passwd
```

Setuid requires careful security consideration.

---

## setgid

On directories, setgid can make new files inherit the directory's group.

Example:

```bash
chmod g+s shared/
```

---

## Sticky bit

Commonly used on shared directories:

```bash
chmod +t shared/
```

The classic example is:

```bash
ls -ld /tmp
```

---

## ACLs

Extended access control lists:

```bash
getfacl file.txt
```

Set an ACL:

```bash
setfacl -m u:alice:r file.txt
```

Remove:

```bash
setfacl -x u:alice file.txt
```

ACLs provide permissions beyond the basic owner/group/other model.

---

# 27. sudo and Root

Run one command as administrator:

```bash
sudo command
```

Open root shell:

```bash
sudo -i
```

Check:

```bash
whoami
```

Exit:

```bash
exit
```

---

## Important security principle

Do not use `sudo` automatically.

Bad habit:

```bash
sudo every_command
```

Better:

```text
Ask:
Why does this operation require administrator privileges?
```

Running software unnecessarily as root increases the potential impact of bugs or malicious code.

---

# 28. Finding Files

## `find`

Current directory:

```bash
find .
```

By name:

```bash
find . -name "*.txt"
```

Files only:

```bash
find . -type f
```

Directories only:

```bash
find . -type d
```

Case-insensitive:

```bash
find . -iname "*.TXT"
```

By size:

```bash
find . -type f -size +100M
```

Modified recently:

```bash
find . -type f -mtime -1
```

Executable files:

```bash
find . -type f -executable
```

---

## Execute a command with find

```bash
find . -name "*.tmp" -delete
```

Use destructive `find` commands carefully.

Safer preview:

```bash
find . -name "*.tmp"
```

---

# 29. Searching File Contents

## grep

```bash
grep "hello" file.txt
```

Case-insensitive:

```bash
grep -i "hello" file.txt
```

Line numbers:

```bash
grep -n "hello" file.txt
```

Recursive:

```bash
grep -R "hello" .
```

Recursive + case insensitive + line number:

```bash
grep -Rni "hello" .
```

Invert match:

```bash
grep -v "hello" file.txt
```

Count matches:

```bash
grep -c "hello" file.txt
```

Show filenames only:

```bash
grep -l "hello" *.txt
```

---

## `grep -E`

Extended regular expressions:

```bash
grep -E "cat|dog" file.txt
```

---

# 30. sort, uniq, wc, cut, tr

## sort

```bash
sort names.txt
```

Reverse:

```bash
sort -r names.txt
```

Numeric:

```bash
sort -n numbers.txt
```

---

## uniq

Remove adjacent duplicates:

```bash
sort names.txt | uniq
```

Count:

```bash
sort names.txt | uniq -c
```

---

## wc

Lines:

```bash
wc -l file.txt
```

Words:

```bash
wc -w file.txt
```

Characters/bytes:

```bash
wc -c file.txt
```

---

## cut

Given:

```text
Alice,ComputerScience,95
Bob,Mathematics,88
```

Extract first field:

```bash
cut -d',' -f1 students.csv
```

Extract third:

```bash
cut -d',' -f3 students.csv
```

---

## tr

Translate characters:

```bash
echo "hello" | tr 'a-z' 'A-Z'
```

Result:

```text
HELLO
```

Delete characters:

```bash
echo "123abc456" | tr -d '0-9'
```

Result:

```text
abc
```

---

# 31. awk

`awk` is a programming language designed around text processing.

Example:

```bash
awk '{print $1}' file.txt
```

Print column 1.

```bash
awk '{print $1, $3}' file.txt
```

Print columns 1 and 3.

CSV:

```bash
awk -F',' '{print $1}' students.csv
```

Condition:

```bash
awk '$3 >= 90 {print $1}' students.txt
```

Print line numbers:

```bash
awk '{print NR, $0}' file.txt
```

Variables:

```bash
awk '{sum += $3} END {print sum}' data.txt
```

`awk` is extremely useful for command-line data processing.

---

# 32. sed

Replace text in output:

```bash
sed 's/apple/orange/g' file.txt
```

Edit the file:

```bash
sed -i 's/apple/orange/g' file.txt
```

Print specific lines:

```bash
sed -n '10,20p' file.txt
```

Delete lines:

```bash
sed '5d' file.txt
```

Multiple commands:

```bash
sed -e 's/a/b/g' -e 's/c/d/g' file.txt
```

---

# 33. Regular Expressions

Regular expressions describe text patterns.

Basic examples:

```text
^       beginning of line
$       end of line
.       any character
*       zero or more of previous pattern
[]      character class
[^]     negated character class
```

Example:

```bash
grep '^A' names.txt
```

Find lines beginning with A.

```bash
grep 'ing$' words.txt
```

Find lines ending with `ing`.

Extended regex:

```bash
grep -E 'cat|dog' file.txt
```

Digit:

```bash
grep -E '[0-9]+' file.txt
```

Regex becomes especially useful with:

```text
grep
sed
awk
find
```

---

# 34. xargs

`xargs` converts input into command arguments.

Example:

```bash
printf '%s\n' a.txt b.txt c.txt | xargs ls -l
```

With `find`:

```bash
find . -name "*.log" -print0 | xargs -0 grep "ERROR"
```

`-print0` and `-0` safely handle filenames containing spaces and special characters.

---

# 35. Processes

A process is a running instance of a program.

---

## ps

Current processes:

```bash
ps
```

All processes:

```bash
ps aux
```

Detailed process tree:

```bash
ps -ef
```

Search:

```bash
ps aux | grep python
```

---

## top

```bash
top
```

Shows:

```text
CPU usage
memory
processes
load
PIDs
```

Quit:

```text
q
```

---

## htop

Install:

```bash
sudo apt install htop
```

Run:

```bash
htop
```

---

## pgrep

```bash
pgrep python
```

Show full command:

```bash
pgrep -af python
```

---

## pidof

```bash
pidof python3
```

---

# 36. Signals

Linux processes can receive signals.

Common signals:

```text
SIGTERM  15    Request graceful termination
SIGKILL   9    Force termination
SIGINT    2    Interrupt, commonly Ctrl+C
SIGHUP    1    Hangup
SIGSTOP  19    Stop process
SIGCONT  18    Continue process
```

Send SIGTERM:

```bash
kill PID
```

Equivalent:

```bash
kill -TERM PID
```

Force:

```bash
kill -KILL PID
```

Usually:

```bash
kill -9 PID
```

should be a last resort rather than the first choice.

---

# 37. Foreground and Background Jobs

Run:

```bash
sleep 100
```

Suspend:

```text
Ctrl+Z
```

Show jobs:

```bash
jobs
```

Continue in background:

```bash
bg
```

Bring to foreground:

```bash
fg
```

Run directly in background:

```bash
sleep 100 &
```

---

## nohup

```bash
nohup long_program > program.log 2>&1 &
```

Useful for processes that should survive terminal logout.

---

# 38. Process Priority

Linux process priority can be adjusted using `nice`.

Run with lower priority:

```bash
nice -n 10 command
```

Change an existing process:

```bash
renice 10 -p PID
```

Priority and scheduling should be used carefully because changing process priorities can affect system responsiveness.

---

# 39. System Monitoring

CPU/process monitor:

```bash
top
```

Memory:

```bash
free -h
```

Disk:

```bash
df -h
```

Directory sizes:

```bash
du -h --max-depth=1
```

CPU information:

```bash
lscpu
```

Memory information:

```bash
lsmem
```

Load average:

```bash
uptime
```

---

## `vmstat`

```bash
vmstat
```

Continuous:

```bash
vmstat 1
```

Useful for observing:

```text
processes
memory
paging
block I/O
CPU
```

---

## `iostat`

May require:

```bash
sudo apt install sysstat
```

Then:

```bash
iostat
```

---

# 40. The /proc Filesystem

`/proc` is a virtual filesystem exposing kernel and process information.

List:

```bash
ls /proc
```

Current process:

```bash
ls /proc/$$
```

CPU:

```bash
cat /proc/cpuinfo
```

Memory:

```bash
cat /proc/meminfo
```

Kernel command line:

```bash
cat /proc/cmdline
```

Process information:

```bash
cat /proc/PID/status
```

Open file descriptors:

```bash
ls -l /proc/PID/fd
```

`/proc` is extremely important for understanding how Linux exposes process and kernel state.

---

# 41. The /sys Filesystem

`/sys` exposes information about devices, drivers, kernel subsystems, and hardware.

Explore:

```bash
ls /sys
```

Devices:

```bash
ls /sys/class
```

Block devices:

```bash
ls /sys/class/block
```

Network interfaces:

```bash
ls /sys/class/net
```

`/sys` is primarily a kernel interface rather than an ordinary storage directory.

---

# 42. Disk Space

## df

Filesystem free space:

```bash
df -h
```

Inodes:

```bash
df -i
```

---

## du

Current directory:

```bash
du -sh .
```

Subdirectories:

```bash
du -h --max-depth=1
```

Sort:

```bash
du -h --max-depth=1 | sort -h
```

---

# 43. Block Devices

List:

```bash
lsblk
```

Detailed:

```bash
lsblk -f
```

Show UUIDs:

```bash
blkid
```

Disk partition table:

```bash
sudo fdisk -l
```

> Disk partitioning commands can destroy data. Never experiment with `fdisk`, `parted`, or formatting commands on important disks without understanding the target device.

---

# 44. Mounting Filesystems

Show mounts:

```bash
mount
```

Show filesystem table:

```bash
cat /etc/fstab
```

Mount a filesystem:

```bash
sudo mount /dev/sdb1 /mnt
```

Unmount:

```bash
sudo umount /mnt
```

Find where a filesystem is mounted:

```bash
findmnt
```

Unmount by device:

```bash
sudo umount /dev/sdb1
```

---

# 45. Archives and Compression

## tar

Create archive:

```bash
tar -cf archive.tar directory/
```

Extract:

```bash
tar -xf archive.tar
```

List:

```bash
tar -tf archive.tar
```

gzip compression:

```bash
tar -czf archive.tar.gz directory/
```

Extract:

```bash
tar -xzf archive.tar.gz
```

---

## bzip2

```bash
tar -cjf archive.tar.bz2 directory/
```

Extract:

```bash
tar -xjf archive.tar.bz2
```

---

## xz

```bash
tar -cJf archive.tar.xz directory/
```

Extract:

```bash
tar -xJf archive.tar.xz
```

---

## zip

```bash
zip -r archive.zip directory/
```

Extract:

```bash
unzip archive.zip
```

---

# 46. Package Management with APT

Update package index:

```bash
sudo apt update
```

Upgrade installed packages:

```bash
sudo apt upgrade
```

Full upgrade:

```bash
sudo apt full-upgrade
```

Install:

```bash
sudo apt install package
```

Remove:

```bash
sudo apt remove package
```

Remove package and configuration files where supported:

```bash
sudo apt purge package
```

Clean unused dependencies:

```bash
sudo apt autoremove
```

Search:

```bash
apt search keyword
```

Show information:

```bash
apt show package
```

Installed packages:

```bash
apt list --installed
```

Upgradeable packages:

```bash
apt list --upgradable
```

---

# 47. dpkg

APT manages repositories and dependencies; `dpkg` handles Debian packages directly.

Install `.deb`:

```bash
sudo dpkg -i package.deb
```

Check package:

```bash
dpkg -l
```

Search installed package database:

```bash
dpkg -l | grep package
```

Show package files:

```bash
dpkg -L package
```

Find which package owns a file:

```bash
dpkg -S /path/to/file
```

Package information:

```bash
dpkg -s package
```

---

# 48. System Services and systemd

List services:

```bash
systemctl list-units --type=service
```

Status:

```bash
systemctl status SERVICE
```

Start:

```bash
sudo systemctl start SERVICE
```

Stop:

```bash
sudo systemctl stop SERVICE
```

Restart:

```bash
sudo systemctl restart SERVICE
```

Enable at boot:

```bash
sudo systemctl enable SERVICE
```

Disable:

```bash
sudo systemctl disable SERVICE
```

Check whether enabled:

```bash
systemctl is-enabled SERVICE
```

Check whether active:

```bash
systemctl is-active SERVICE
```

---

# 49. System Logs

## journalctl

All journal entries:

```bash
journalctl
```

Recent:

```bash
journalctl -n 100
```

Follow live:

```bash
journalctl -f
```

Current boot:

```bash
journalctl -b
```

Previous boot:

```bash
journalctl -b -1
```

Specific service:

```bash
journalctl -u SERVICE
```

Recent service logs:

```bash
journalctl -u SERVICE -n 100
```

Since a time:

```bash
journalctl --since "1 hour ago"
```

---

## dmesg

Kernel messages:

```bash
dmesg
```

Recent:

```bash
dmesg | tail -50
```

Human-readable timestamps:

```bash
dmesg -T
```

---

# 50. Networking Fundamentals

Important concepts:

```text
IP address
MAC address
subnet
gateway
DNS
TCP
UDP
port
socket
routing
```

---

# 51. Network Interfaces

Show interfaces:

```bash
ip addr
```

Short:

```bash
ip a
```

Show links:

```bash
ip link
```

Show routes:

```bash
ip route
```

Show routing table:

```bash
ip route show
```

---

## NetworkManager

Ubuntu desktop systems commonly use NetworkManager.

Show connections:

```bash
nmcli connection show
```

Show devices:

```bash
nmcli device status
```

Show general status:

```bash
nmcli general status
```

---

# 52. DNS

Test name resolution:

```bash
getent hosts example.com
```

Depending on installed tools:

```bash
dig example.com
```

or:

```bash
nslookup example.com
```

Install DNS utilities if necessary:

```bash
sudo apt install dnsutils
```

---

# 53. Ports and Sockets

Show listening TCP/UDP sockets:

```bash
ss -tulpn
```

Options:

```text
-t    TCP
-u    UDP
-l    listening
-p    process
-n    numeric
```

Find a port:

```bash
sudo lsof -i :8080
```

---

# 54. SSH

Connect:

```bash
ssh user@host
```

Example:

```bash
ssh student@192.168.1.20
```

Specify port:

```bash
ssh -p 2222 user@host
```

Verbose debugging:

```bash
ssh -v user@host
```

More verbose:

```bash
ssh -vvv user@host
```

Generate SSH key:

```bash
ssh-keygen
```

Copy public key:

```bash
ssh-copy-id user@host
```

Then login can often use:

```bash
ssh user@host
```

without entering a password every time, depending on server configuration.

---

# 55. Secure File Transfer

## scp

Copy file:

```bash
scp file.txt user@host:/tmp/
```

Copy directory:

```bash
scp -r project/ user@host:~/project/
```

---

## sftp

```bash
sftp user@host
```

Common commands inside SFTP:

```text
ls
cd
pwd
get
put
mkdir
rm
exit
```

---

## rsync

Synchronize:

```bash
rsync -av source/ destination/
```

Remote:

```bash
rsync -av project/ user@host:~/project/
```

Dry run:

```bash
rsync -av --dry-run source/ destination/
```

`--dry-run` is excellent for learning what a synchronization command will do before actually changing files.

---

# 56. curl and wget

## curl

Download:

```bash
curl -O https://example.com/file.txt
```

Display webpage/API response:

```bash
curl https://example.com
```

Headers:

```bash
curl -I https://example.com
```

Follow redirects:

```bash
curl -L https://example.com
```

POST data:

```bash
curl -X POST -d "name=Alice" https://example.com/api
```

---

## wget

Download:

```bash
wget https://example.com/file.zip
```

Continue download:

```bash
wget -c https://example.com/file.zip
```

Recursive website retrieval has powerful options and should be used carefully.

---

# 57. Network Diagnostics

## ping

```bash
ping example.com
```

Count:

```bash
ping -c 4 example.com
```

---

## traceroute

```bash
traceroute example.com
```

May require:

```bash
sudo apt install traceroute
```

---

## tracepath

```bash
tracepath example.com
```

---

## hostname

```bash
hostname
```

IP resolution:

```bash
hostname -I
```

---

## ip

```bash
ip addr
ip route
ip neigh
```

Neighbor table:

```bash
ip neigh
```

---

# 58. Bash Scripting

Create:

```bash
nano hello.sh
```

Content:

```bash
#!/bin/bash

# This is a comment.
# The first line tells Linux to execute the script with Bash.

echo "Hello, Linux!"
```

Make executable:

```bash
chmod +x hello.sh
```

Run:

```bash
./hello.sh
```

Or:

```bash
bash hello.sh
```

---

# 59. Shell Variables

```bash
name="Alice"
echo "$name"
```

Do not put spaces around `=`:

Correct:

```bash
name="Alice"
```

Incorrect:

```bash
name = "Alice"
```

Export:

```bash
export name
```

---

# 60. Script Arguments

Run:

```bash
./script.sh Alice 20
```

Inside:

```bash
echo "$1"
echo "$2"
```

Special variables:

```text
$0       script name
$1       first argument
$2       second argument
$#       number of arguments
$@       all arguments
$?       previous exit status
$$       current shell PID
```

---

# 61. Conditions

File exists:

```bash
if [ -f file.txt ]; then
    echo "File exists"
fi
```

Directory:

```bash
if [ -d project ]; then
    echo "Directory exists"
fi
```

String comparison:

```bash
if [ "$name" = "Alice" ]; then
    echo "Hello Alice"
fi
```

Numeric comparison:

```bash
if [ "$age" -ge 18 ]; then
    echo "Adult"
fi
```

Common tests:

```text
-f    regular file
-d    directory
-e    exists
-r    readable
-w    writable
-x    executable
```

---

# 62. Loops

## for

```bash
for file in *.txt; do
    echo "$file"
done
```

---

## C-style for

```bash
for ((i=0; i<10; i++)); do
    echo "$i"
done
```

---

## while

```bash
i=0

while [ "$i" -lt 5 ]; do
    echo "$i"
    i=$((i + 1))
done
```

---

## until

```bash
i=0

until [ "$i" -ge 5 ]; do
    echo "$i"
    i=$((i + 1))
done
```

---

# 63. Functions

```bash
greet() {
    echo "Hello, $1"
}
```

Call:

```bash
greet "Alice"
```

Return status:

```bash
check_file() {
    if [ -f "$1" ]; then
        return 0
    else
        return 1
    fi
}
```

---

# 64. Arrays

Create:

```bash
names=("Alice" "Bob" "Charlie")
```

First element:

```bash
echo "${names[0]}"
```

All:

```bash
echo "${names[@]}"
```

Number:

```bash
echo "${#names[@]}"
```

Loop:

```bash
for name in "${names[@]}"; do
    echo "$name"
done
```

---

# 65. Command Substitution

Run a command and store its output:

```bash
today=$(date)
echo "$today"
```

Example:

```bash
files=$(ls)
echo "$files"
```

Prefer:

```bash
$(command)
```

over the older:

```bash
`command`
```

---

# 66. Arithmetic

```bash
a=10
b=20

sum=$((a + b))

echo "$sum"
```

Other operators:

```text
+
-
*
/
%
```

Example:

```bash
((count++))
```

---

# 67. Shell Input

Read user input:

```bash
read -p "Enter your name: " name
echo "Hello $name"
```

Read securely:

```bash
read -s -p "Password: " password
echo
```

---

# 68. Signals and Traps in Scripts

A script can react to signals.

Example:

```bash
cleanup() {
    echo "Cleaning up..."
}

trap cleanup EXIT
```

Temporary directory example:

```bash
tmpdir=$(mktemp -d)

cleanup() {
    rm -rf "$tmpdir"
}

trap cleanup EXIT
```

This is an important pattern for robust shell scripts.

---

# 69. Debugging Bash Scripts

Run with tracing:

```bash
bash -x script.sh
```

Inside script:

```bash
set -x
```

Stop tracing:

```bash
set +x
```

Useful strict mode:

```bash
set -euo pipefail
```

Meaning approximately:

```text
-e    exit when a command fails
-u    error on unset variables
-o pipefail    propagate pipeline failures
```

Be aware that `set -e` has subtle Bash behavior. Students should learn how exit statuses and conditional commands interact rather than treating `set -e` as magic.

---

# 70. Cron and Scheduled Tasks

List your cron jobs:

```bash
crontab -l
```

Edit:

```bash
crontab -e
```

Example:

```text
0 2 * * * /home/student/backup.sh
```

Meaning:

```text
minute   hour   day   month   weekday
  0       2      *      *        *
```

Runs every day at 02:00.

---

## systemd timers

Modern Ubuntu also supports systemd timers.

List:

```bash
systemctl list-timers
```

Timers are often preferable for system-level scheduled services because they integrate with systemd logging and dependencies.

---

# 71. System Information

Kernel:

```bash
uname -a
```

Kernel release:

```bash
uname -r
```

Ubuntu release:

```bash
lsb_release -a
```

CPU:

```bash
lscpu
```

Memory:

```bash
free -h
```

PCI:

```bash
lspci
```

USB:

```bash
lsusb
```

Architecture:

```bash
uname -m
```

---

# 72. Time and Date

Current time:

```bash
date
```

UTC:

```bash
date -u
```

Formatted:

```bash
date '+%Y-%m-%d %H:%M:%S'
```

Timezone:

```bash
timedatectl
```

Set system time:

```bash
sudo timedatectl set-time ...
```

Changing system time should normally be done only with appropriate administrator privileges and an understanding of time synchronization.

---

# 73. Users, Sessions, and Login Information

Current user:

```bash
whoami
```

Logged-in users:

```bash
who
```

More detail:

```bash
w
```

Login history:

```bash
last
```

User ID:

```bash
id
```

Current shell:

```bash
echo "$SHELL"
```

---

# 74. Process and Resource Limits

Show limits:

```bash
ulimit -a
```

Maximum open files:

```bash
ulimit -n
```

Processes can also be constrained by systemd resource controls and cgroups.

---

# 75. Shared Libraries

Linux programs often depend on shared libraries.

Check dependencies:

```bash
ldd /bin/ls
```

Find library cache:

```bash
ldconfig -p
```

Show executable type:

```bash
file /bin/ls
```

This is useful when learning how compiled programs depend on system libraries.

---

# 76. Compilers and Build Tools

Ubuntu can install a standard development environment:

```bash
sudo apt install build-essential
```

This typically provides tools such as:

```text
gcc
g++
make
```

Check GCC:

```bash
gcc --version
```

Check G++:

```bash
g++ --version
```

---

## Compile C

```bash
gcc hello.c -o hello
```

Run:

```bash
./hello
```

Compile C++:

```bash
g++ hello.cpp -o hello
```

---

## make

```bash
make
```

Clean if a Makefile provides the target:

```bash
make clean
```

---

# 77. Environment and Development Tools

Useful commands for programmers:

```bash
gcc
g++
make
cmake
pkg-config
ldd
ldconfig
nm
objdump
readelf
strings
```

---

## `readelf`

Inspect ELF binaries:

```bash
readelf -h program
```

Sections:

```bash
readelf -S program
```

---

## `nm`

Show symbols:

```bash
nm program
```

---

## `strings`

Extract printable strings:

```bash
strings program
```

---

## `objdump`

Disassemble:

```bash
objdump -d program
```

These tools are useful when studying:

```text
compilers
linkers
object files
ELF
assembly
debugging
operating systems
```

---

# 78. Git

Configure identity:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

Clone:

```bash
git clone URL
```

Status:

```bash
git status
```

Diff:

```bash
git diff
```

Stage:

```bash
git add file.txt
```

Stage everything:

```bash
git add .
```

Commit:

```bash
git commit -m "Add assignment"
```

History:

```bash
git log
```

Compact history:

```bash
git log --oneline
```

Pull:

```bash
git pull
```

Push:

```bash
git push
```

Branches:

```bash
git branch
```

Create/switch:

```bash
git switch -c feature
```

Switch:

```bash
git switch main
```

Merge:

```bash
git merge feature
```

Remote:

```bash
git remote -v
```

---

# 79. Checksums and File Integrity

MD5:

```bash
md5sum file.iso
```

SHA-256:

```bash
sha256sum file.iso
```

SHA-512:

```bash
sha512sum file.iso
```

Verify a downloaded file:

```bash
sha256sum file.iso
```

Compare the result with a trusted published checksum.

Checksums are useful for:

```text
integrity checking
download verification
backup verification
software distribution
```

---

# 80. Encryption Basics

Linux commonly uses OpenSSL and GnuPG.

Check:

```bash
openssl version
```

GPG:

```bash
gpg --version
```

Generate a GPG key:

```bash
gpg --full-generate-key
```

List keys:

```bash
gpg --list-keys
```

GPG is a large topic by itself; students should understand the difference between:

```text
hashing
encryption
digital signatures
authentication
```

---

# 81. Permissions and Security Diagnostics

Check permissions:

```bash
ls -l
```

Check ownership:

```bash
stat file.txt
```

Check ACL:

```bash
getfacl file.txt
```

Check current identity:

```bash
id
```

Check sudo access:

```bash
sudo -l
```

Find SUID files:

```bash
find / -perm -4000 -type f 2>/dev/null
```

This is useful for security education, but students should understand why SUID binaries require special attention.

---

# 82. Symbolic Links and Hard Links

## Symbolic link

```bash
ln -s target link
```

Inspect:

```bash
ls -l link
```

---

## Hard link

```bash
ln original hardlink
```

Both names refer to the same inode.

Check inode:

```bash
ls -li original hardlink
```

Conceptual difference:

```text
Symbolic link:
name → path → target

Hard link:
name ─┐
      ├── inode → data
name ─┘
```

Hard links generally cannot cross filesystems and normally cannot be created for directories by ordinary users.

---

# 83. File Descriptors

Linux processes commonly use:

```text
0 = stdin
1 = stdout
2 = stderr
```

See file descriptors for a process:

```bash
ls -l /proc/PID/fd
```

Example:

```bash
echo "hello" > output.txt
```

Redirect stdout:

```bash
command 1>output.txt
```

Redirect stderr:

```bash
command 2>errors.txt
```

Both:

```bash
command >output.txt 2>errors.txt
```

This is fundamental to Unix process I/O.

---

# 84. Named Pipes and IPC

Create FIFO:

```bash
mkfifo mypipe
```

Terminal 1:

```bash
cat mypipe
```

Terminal 2:

```bash
echo "Hello" > mypipe
```

The first terminal receives:

```text
Hello
```

Named pipes are one form of inter-process communication.

Other Linux IPC mechanisms include:

```text
pipes
FIFOs
signals
shared memory
message queues
sockets
Unix domain sockets
```

---

# 85. Terminal Control

Interrupt:

```text
Ctrl+C
```

Suspend:

```text
Ctrl+Z
```

End input:

```text
Ctrl+D
```

Clear screen:

```text
Ctrl+L
```

Search command history:

```text
Ctrl+R
```

Move to beginning of line:

```text
Ctrl+A
```

Move to end:

```text
Ctrl+E
```

Delete previous word:

```text
Ctrl+W
```

Clear current line:

```text
Ctrl+U
```

---

# 86. tmux

Install:

```bash
sudo apt install tmux
```

Start:

```bash
tmux
```

Detach:

```text
Ctrl+B then D
```

Reattach:

```bash
tmux attach
```

New window:

```text
Ctrl+B then C
```

Split vertically:

```text
Ctrl+B then %
```

Split horizontally:

```text
Ctrl+B then "
```

tmux is useful for remote administration, development, servers, and long-running terminal sessions.

---

# 87. Common Command-Line Utilities

Important general-purpose commands:

```bash
basename
dirname
realpath
readlink
basename
printf
echo
seq
yes
sleep
true
false
env
printenv
tee
xargs
watch
time
timeout
script
screen
tmux
```

---

## `basename`

```bash
basename /home/student/file.txt
```

Result:

```text
file.txt
```

---

## `dirname`

```bash
dirname /home/student/file.txt
```

Result:

```text
/home/student
```

---

## `realpath`

```bash
realpath file.txt
```

Shows the absolute resolved path.

---

## `readlink`

```bash
readlink link
```

Resolve symbolic links:

```bash
readlink -f link
```

---

## `printf`

More predictable formatting than `echo`:

```bash
printf "Name: %s\n" "Alice"
```

---

## `seq`

```bash
seq 1 10
```

---

## `sleep`

```bash
sleep 5
```

---

## `time`

Measure execution time:

```bash
time ls
```

---

## `timeout`

Stop a command after a limit:

```bash
timeout 10s long_program
```

---

## `tee`

Display and save simultaneously:

```bash
command | tee output.txt
```

Append:

```bash
command | tee -a output.txt
```

---

# 88. Advanced Command Combinations

## Find large files

```bash
find . -type f -size +100M -exec ls -lh {} \;
```

---

## Search source code

```bash
grep -Rni --include="*.c" "malloc" .
```

---

## Count file types

```bash
find . -type f -name "*.py" | wc -l
```

---

## Find the largest directories

```bash
du -h --max-depth=1 | sort -h
```

---

## Find running Python programs

```bash
ps aux | grep '[p]ython'
```

The `[p]ython` trick prevents the grep command itself from appearing as a match.

---

## Monitor a log for errors

```bash
tail -f application.log | grep -Ei 'error|failed|critical'
```

---

## Find files and search them

```bash
find . -type f -name "*.txt" -print0 | xargs -0 grep -n "Linux"
```

---

## Save command output and display it

```bash
ls -lah | tee files.txt
```

---

# 89. Linux Troubleshooting Method

Do not randomly run commands.

Use a structured process.

## Step 1 — Define the problem

Example:

```text
A program will not start.
```

---

## Step 2 — Verify the obvious

```bash
pwd
ls -lah
which program
program --version
```

---

## Step 3 — Check permissions

```bash
ls -l program
id
```

---

## Step 4 — Check dependencies

For compiled programs:

```bash
ldd program
```

For packages:

```bash
apt policy package
```

---

## Step 5 — Check processes

```bash
ps aux
pgrep -af program
```

---

## Step 6 — Check ports

```bash
ss -tulpn
```

---

## Step 7 — Check logs

```bash
journalctl
```

---

## Step 8 — Check system resources

```bash
free -h
df -h
top
```

---

## Step 9 — Check networking

```bash
ip a
ip route
ping host
```

---

## Step 10 — Reproduce the failure

Run the smallest command that demonstrates the problem.

Then investigate the exact error.

---

# 90. Essential Command Cheat Sheet

## Navigation

```bash
pwd
ls
ls -lah
cd
cd ..
cd -
cd ~
```

## Files

```bash
touch
mkdir
mkdir -p
cp
cp -r
mv
rm
rm -r
```

## Reading

```bash
cat
less
head
tail
tail -f
```

## Search

```bash
find
grep
grep -R
which
whereis
```

## Text processing

```bash
sort
uniq
wc
cut
tr
awk
sed
xargs
```

## Permissions

```bash
ls -l
chmod
chown
chgrp
getfacl
setfacl
```

## Users

```bash
whoami
id
groups
who
w
last
```

## Processes

```bash
ps
top
htop
pgrep
pidof
kill
pkill
killall
nice
renice
```

## System

```bash
uname
lsb_release
lscpu
free
uptime
vmstat
```

## Storage

```bash
df
du
lsblk
blkid
mount
umount
findmnt
```

## Packages

```bash
apt
apt-cache
dpkg
```

## Services/logs

```bash
systemctl
journalctl
dmesg
```

## Network

```bash
ip
ping
ss
curl
wget
dig
nslookup
traceroute
ssh
scp
sftp
rsync
```

## Archives

```bash
tar
gzip
gunzip
zip
unzip
```

## Development

```bash
gcc
g++
make
cmake
ldd
readelf
nm
objdump
strings
gdb
```

## Shell

```bash
bash
source
export
alias
env
printenv
printf
read
```

## Git

```bash
git clone
git status
git add
git commit
git log
git diff
git branch
git switch
git merge
git pull
git push
```

---

# 91. University Practice Exercises

## Exercise 1 — Navigation

Create:

```text
~/linux-course/
├── week01/
├── week02/
└── assignments/
```

Commands:

```bash
mkdir -p ~/linux-course/{week01,week02,assignments}
```

Navigate through them using:

```bash
cd
pwd
ls
cd ..
cd -
```

---

## Exercise 2 — File Operations

Create:

```bash
touch ~/linux-course/week01/{a.txt,b.txt,c.txt}
```

Copy:

```bash
cp ~/linux-course/week01/a.txt ~/linux-course/week01/a_backup.txt
```

Rename:

```bash
mv ~/linux-course/week01/b.txt ~/linux-course/week01/b_final.txt
```

---

## Exercise 3 — Permissions

Create:

```bash
echo '#!/bin/bash' > test.sh
echo 'echo Hello' >> test.sh
```

Try:

```bash
./test.sh
```

It may fail because it is not executable.

Fix:

```bash
chmod +x test.sh
```

Run:

```bash
./test.sh
```

---

## Exercise 4 — Pipes

Run:

```bash
ps aux | grep bash
```

Then:

```bash
ps aux | grep bash | wc -l
```

Explain what each stage does.

---

## Exercise 5 — Redirection

Run:

```bash
ls -lah > listing.txt
```

Then:

```bash
cat listing.txt
```

Append:

```bash
date >> listing.txt
```

---

## Exercise 6 — grep

Create:

```bash
printf "Alice\nBob\nCharlie\nAndrew\n" > names.txt
```

Find names beginning with A:

```bash
grep '^A' names.txt
```

---

## Exercise 7 — awk

Create:

```text
Alice 90
Bob 75
Charlie 95
David 82
```

Save as:

```text
grades.txt
```

Print names:

```bash
awk '{print $1}' grades.txt
```

Print students with grades >= 90:

```bash
awk '$2 >= 90 {print $1}' grades.txt
```

---

## Exercise 8 — Processes

Run:

```bash
sleep 300 &
```

Find:

```bash
pgrep -af sleep
```

Terminate:

```bash
kill PID
```

---

## Exercise 9 — Disk Investigation

Run:

```bash
df -h
```

Then:

```bash
du -h --max-depth=1 ~ | sort -h
```

Identify which directories consume the most space.

---

## Exercise 10 — Networking

Run:

```bash
ip a
ip route
```

Then:

```bash
ping -c 4 8.8.8.8
```

Then:

```bash
getent hosts example.com
```

Explain:

```text
IP address
default gateway
DNS
```

---

## Exercise 11 — Bash Script

Create:

```bash
nano system_info.sh
```

Write a script that displays:

```text
username
hostname
date
kernel version
disk usage
memory usage
```

Useful commands:

```bash
whoami
hostname
date
uname -r
df -h
free -h
```

---

## Exercise 12 — File Search

Find all `.txt` files below your home directory:

```bash
find ~ -type f -name "*.txt"
```

Then find files larger than 1 MB:

```bash
find ~ -type f -size +1M
```

---

## Exercise 13 — Git

Create a project:

```bash
mkdir git-practice
cd git-practice
git init
```

Create:

```bash
echo "Hello Linux" > README.md
```

Then:

```bash
git status
git add README.md
git commit -m "Initial commit"
git log --oneline
```

---

# 92. Suggested Semester Progression

## Week 1 — Linux and Terminal

Learn:

```text
terminal
shell
pwd
ls
cd
mkdir
touch
cp
mv
rm
```

Assignment:

> Create and manage a directory tree entirely from the command line.

---

## Week 2 — Files and Text

Learn:

```text
cat
less
head
tail
grep
find
sort
uniq
wc
cut
```

Assignment:

> Analyze a text dataset using only command-line tools.

---

## Week 3 — Pipes and Redirection

Learn:

```text
|
>
>>
<
2>
2>&1
tee
```

Assignment:

> Build command pipelines that transform and summarize text.

---

## Week 4 — Permissions

Learn:

```text
users
groups
chmod
chown
chgrp
sudo
ACL
```

Assignment:

> Build a shared directory with controlled user/group access.

---

## Week 5 — Processes

Learn:

```text
ps
top
htop
pgrep
kill
signals
jobs
bg
fg
nice
```

Assignment:

> Launch, monitor, suspend, resume, and terminate processes.

---

## Week 6 — Bash Scripting

Learn:

```text
variables
arguments
if
for
while
functions
arrays
exit status
```

Assignment:

> Write a command-line backup or file-analysis program.

---

## Week 7 — Advanced Text Processing

Learn:

```text
regex
grep -E
sed
awk
xargs
```

Assignment:

> Analyze structured log data.

---

## Week 8 — Storage

Learn:

```text
df
du
lsblk
mount
umount
findmnt
tar
gzip
zip
```

Assignment:

> Create and verify compressed backups.

---

## Week 9 — Package Management and systemd

Learn:

```text
apt
dpkg
systemctl
journalctl
```

Assignment:

> Install software, inspect a service, and analyze its logs.

---

## Week 10 — Networking

Learn:

```text
ip
ping
ss
DNS
curl
wget
ssh
scp
rsync
```

Assignment:

> Diagnose a simulated network problem and transfer files between machines.

---

## Week 11 — Development Tools

Learn:

```text
gcc
g++
make
cmake
ldd
gdb
readelf
nm
objdump
```

Assignment:

> Compile and debug a small C/C++ program.

---

## Week 12 — Git and Software Engineering

Learn:

```text
git clone
git status
git diff
git add
git commit
git branch
git switch
git merge
git pull
git push
```

Assignment:

> Manage a multi-version programming project with Git.

---

# Final Linux Mental Model

A strong CS student should gradually understand Linux at several layers:

```text
┌─────────────────────────────────────────┐
│ Applications                            │
│ Python / C / C++ / Java / editors       │
├─────────────────────────────────────────┤
│ Shell                                   │
│ Bash / pipes / redirection / scripting  │
├─────────────────────────────────────────┤
│ Processes                               │
│ PID / signals / scheduling / jobs       │
├─────────────────────────────────────────┤
│ Filesystem                              │
│ files / directories / inode / links     │
├─────────────────────────────────────────┤
│ Permissions                             │
│ users / groups / ACL / sudo             │
├─────────────────────────────────────────┤
│ Networking                              │
│ IP / TCP / UDP / DNS / sockets          │
├─────────────────────────────────────────┤
│ Services                                │
│ systemd / journal / daemons             │
├─────────────────────────────────────────┤
│ Storage                                 │
│ partitions / filesystems / mounts      │
├─────────────────────────────────────────┤
│ System interfaces                       │
│ /proc / /sys / device files             │
├─────────────────────────────────────────┤
│ Linux Kernel                            │
└─────────────────────────────────────────┘
```

The ultimate goal is not to memorize commands.

The goal is to understand the relationship:

```text
COMMAND
   ↓
SHELL
   ↓
PROCESS
   ↓
SYSTEM CALLS
   ↓
KERNEL
   ↓
CPU / MEMORY / STORAGE / NETWORK
```

Once students understand this model, Linux commands become much easier to learn because each command has a place in the operating-system architecture.

---

# Final Command Learning Strategy

Students should memorize the basic commands:

```bash
pwd
ls
cd
mkdir
touch
cp
mv
rm
cat
less
head
tail
grep
find
chmod
chown
sudo
ps
kill
top
df
du
ip
ping
ssh
tar
apt
systemctl
journalctl
```

Then learn the Unix composition model:

```bash
command1 | command2 | command3
```

Then learn shell programming:

```bash
variables
conditions
loops
functions
exit codes
```

Then learn system internals:

```text
processes
signals
file descriptors
/proc
/sys
sockets
permissions
systemd
```

Finally, learn to troubleshoot systematically:

```text
What am I trying to do?
        ↓
What command should perform it?
        ↓
What did the command actually do?
        ↓
What exit status did it return?
        ↓
What process is involved?
        ↓
What resources does it use?
        ↓
What does the system log say?
        ↓
What layer is actually failing?
```

That is the core command-line skill every computer science student should develop.
