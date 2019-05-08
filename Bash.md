# Bash

任务：

- 理解变量、条件语句、循环语句、标准输入输出、I/O重定向、管道、函数等概念
- 能编写脚本，组合常用Linux工具完成简单工作
- 尝试用Shell写些小程序，统计某工作目录及其子目录下.c文件一共有多少行，统计某文件中出现最多的10个单词的次数

## Bash and Bash scripts

### Common shell programs

The shell reads commands from the script line per line and searches for those commands on the system.

UNIX system will usually offer a variety of shell types:

- **sh**, Bourne Shell, the basic shell, a small program with few features.
- **bash**, Bourne Again shell, the standard GNU shell, intuitive and flexible, a *superset* of the Bourne shell. 
- **csh**, C shell, the syntax of this shell resembles that of the C programming language.
- **tcsh**, TENEX C Shell, a superset of the common C shell.
- **ksh**, Korn shell, sometimes appreciated by people with a UNIX background.

The file `/etc/shells` gives an overview of known shells on a Linux system.

```shell
$ cat /etc/shells
/bin/bash
/bin/sh
/bin/tcsh
/bin/csh
```

Your default shell is set in the `/etc/passwd` file.

```shell
mia:L2NOfqdlPrHwE:504:504:Mia Maya:/home/mia:/bin/bash
```

### Executing commands

Bash determines the type of program that is to be executed, normal compiled program and built-in commands. When executing a normal program, Bash forks a child process to execute it. In contrast, built-in commands are executed directly.

Bash supports 3 types of built-in commands:

- Bourne Shell built-ins:

  **:**, **.**, **break**, **cd**, **continue**, **eval**, **exec**, **exit**, **export**, **getopts**, **hash**, **pwd**, **readonly**, **return**, **set**, **shift**, **test**, **[**, **times**, **trap**, **umask** and **unset**.

- Bash built-in commands:

  **alias**, **bind**, **builtin**, **command**, **declare**, **echo**, **enable**, **help**, **let**, **local**, **logout**, **printf**, **read**, **shopt**, **type**, **typeset**, **ulimit** and **unalias**.

- Special built-in commands (ignored).

### Working process

If input is not commented, the shell reads it and divides it into words and operators, employing quoting rules to define the meaning of each character of input. Then these words and operators are translated into commands and other constructs, which return an exit status available for inspection or processing.

### Developing good scripts

Properties of good scripts:

- A script should run without errors.
- It should perform the task for which it is intended.
- Program logic is clearly defined and apparent.
- A script does not do unnecessary work.
- Scripts should be reusable.

## Writing and debugging scripts

### Creating and running a script

First, create a file to contain a a sequence of commands, which is called a script.

```shell
# script1.sh
#! /bin/bash
clear
echo "The script starts now."
echo "Hi, $USER!"
echo
echo "I will now fetch you a list of connected users:"
echo 
w
echo
echo "I'm setting two varibales now."
COLOR="BLACK"
VALUE="9"
echo "This is a string: $COLOR"
echo "And this is a number: $VALUE"
echo 
echo "ByeBye!"
```

And then execute it:

```shell
chmod +x script1.sh
./script1.sh
```

If you want you setup a subshell to execute:

```shell
rbash script1.sh
sh script1.sh
bash -x script1.sh
```

Or, you just want to execute it in current shell:

```shell
source script1.sh
```

### Script basics

The first line of the script determines the shell to start. The first two characters of the first line should be *#!*, then follows the path to the shell that should interpret the commands that follow. Blank lines are also considered to be lines, so don't start your script with an empty line.

To specify `bash` as the execute shell:

```shell
#!/bin/bash
```

Comments are useful to enlighten the reader. Everything the shell encounters after a hash mark on a line is ignored and only visible upon opening the shell script file.

```shell
# This script clears the terminal, displays a greeting and gives information
# about currently connected users.  The two example variables are set and displayed.
```

### Debugging Bash scripts

Bash provides extensive debugging features. The most common is to start up the subshell with the `-x` option, which will run the entire script in debug mode. Traces of each command plus its arguments are printed to standard output after the commands have been expanded but before they are executed.

```shell
$ bash -x script1.sh
+ echo 'Hi, youwu!'
Hi, youwu!
+echo

+echo "I will now fetch you a list of connected users:"
I will now fetch you a list of connected users:
...
```

We can debug only the specified part, by adding `set -x` and `set +x`. For example, Say we are not sure what the **w** command will do in the example `commented-script1.sh`, then we could enclose it in the script like this:

```shell
set -x			# activate debugging from here
w
set +x			# stop debugging from here
```

Output then looks like this:

```shell
Hi, youwu!

I will now fetch you a list of connected users:

+ w
  21:57:52  up 1 day,  7:00,  1 user,  load average: 0.00, 0.01, 0.00
USER     TTY      FROM              LOGIN@   IDLE   JCPU   PCPU  WHAT
youwu     tty2    :0                273月19  29days  4:22  0.06s  /usr/lib/tracke
+ set +x

I'm setting two variables now.
```

## The Bash environment







## 参考文献

1. [Bash Guide for Beginners](http://www.tldp.org/LDP/Bash-Beginners-Guide/html/index.html)