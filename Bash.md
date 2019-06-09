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

### Shell initialization files

System-wide configuration files are `/etc/profile` and `/etc/bashrc`.

- When invoked interactively with the `--login` option or when invoked as **sh**, Bash reads the `/etc/profile` instructions. These usually set the shell variables `PATH`, `USER`, `MAIL`, `HOSTNAME` and `HISTSIZE`.

- Since `/etc/profile` is read by all other shells, it might be better to put Bash-specific configurations in `/etc/bashrc`. `/etc/bashrc` usually contains system-wide definitions for shell functions and aliases. 

Besides, each user can configure their own shell using `~/.bash_profile`, `~/.bash_login`, `~/profile` and `~/.bashrc` and `~/.bash_logout`. 

- `~/.bash_profile` is the preferred configuration file for configuring user environments individually. 

- `~/.bash_login` contains specific settings that are normally only executed when logging into the system. 
- In the absence of `~/.bash_profile` and `~/.bash_login`, `~/.profile` is read. It can hold the same configurations, which are then also accessible by other shells.
- Today, it is more common to use a non-login shell, for instance when logged in graphically using X terminal windows. Upon opening such a window, the user does not have to provide a user name or password; no authentication is done. Bash searches for `~/.bashrc` when this happens, so it is referred to in the files read upon login as well, which means you don't have to enter the same settings in multiple files.
- `~/.bash_logout` contains specific instructions for the logout procedure.

### Variables

#### Types of variables

Bash keeps a list of two types of variables: Global variables and Local variables.

Global variables or environment variables are available in all shells. The **env** or **printenv** commands can be used to display environment variables.

Local variables are only available in the current shell. Using the **set** built-in command without any options will display a list of all variables (including environment variables) and functions.

#### Creating variables

Variables are case sensitive and capitalized by default. Variables can also contain digits, but a name starting with a digit is not allowed.

To set a variable in the shell, use below. Putting spaces around the equal sign will cause errors. It is a good habit to quote content strings when assigning values to variables

```shell
VARNAME="value"
```

A variable created like the ones in the example above is only available to the current shell. Child processes of the current shell will not be aware of this variable as well. In order to pass variables to a subshell, we need to *export* them using the **export** built-in command. A subshell can change variables it inherited from the parent, but the changes made by the child don't affect the parent. 

```shell
export VARNAME="value"
```

Remove a variable.

```shell
unset VARNAME
```

#### Reserved variables

Bash use some reserved variables, such as PATH, HOME, PWD, PPID, UID, etc. Check them in [website](http://www.tldp.org/LDP/Bash-Beginners-Guide/html/sect_03_02.html).

#### Special parameters

The shell treats several parameters specially. These parameters may only be referenced; assignment to them is not allowed,such as $*, S!, etc. Check them in [website](https://www.cnblogs.com/chjbbs/p/6393805.html).

### Quoting characters

Quoting is used to remove the special meaning of characters or words: quotes can disable special treatment for special characters. Quoting characters in Bash are `\`, `'`, `"`.

Escape characters, `\` in Bash, are used to remove the special meaning from a single character. It preserves the literal value of the next character that follows, with the exception of *newline* which marks the continuation of a line.

```shell
$ date=20021226
$ echo $date
20021226
$ echo \$date
$date
```

Single quotes ('') are used to preserve the literal value of each character enclosed within the quotes. A single quote may not occur between single quotes, even when preceded by a backslash.

```shell
$ echo '$date'
$date
```

Using double quotes the literal value of all characters enclosed is preserved, except for the dollar sign, the backticks (backward single quotes, ``) and the backslash.

```shell
$ echo "$date"
20021226
$ echo "`date`"
2019年 05月 14日 星期二 21:53:49 CST
$ echo "I'd say: \"Go for it!\""
I'd say: "Go for it!"
$ echo "\"
More input>"
$ echo "\\"
\
```

### Shell expansion

After the command has been split into *tokens*, these tokens or words are expanded or resolved. There are eight kinds of expansion performed.

- Brace expansion

  Brace expansion is a mechanism by which arbitrary strings may be generated. 

  ```shell
  $ echo sp{el,il,al}l
  spell spill spall
  $ echo class{1..3} is great
  class1 class2 class3 is great
  ```

- Tilde expansion

  If none of the characters in the tilde-prefix are quoted, the characters in the tilde-prefix following the tilde are treated as a possible login name. `~ => HOME，~+ => PWD，~- => OLDPWD`

  ```shell
  $ echo abc~ ~def
  abc~ ~def
  $ echo ~ ~/work
  /home/youwu /home/youwu/work
  $ echo $PWD $OLDPWD
  /home/youwu/work/scripts /home/youwu/work
  $ echo ~+ ~-
  /home/youwu/work/scripts /home/youwu/work
  ```

- Shell parameter and variable expansion

  The parameter name or symbol to be expanded may be enclosed in braces, which are optional but serve to protect the variable to be expanded from characters immediately following it which could be interpreted as part of the name.

  ```shell
  echo $HOME ${HOME}abc
  /home/youwu /home/youwuabc
  echo ${EIEIEI:-undefined} $EIEIEI
  undefined
  echo ${EIEIEI:= lalalala} $EIEIEI
  lalalala lalalala
  echo ${HOME:6} ${HOME:1:4}
  youwu home
  echo ${!HO*}
  HOME HOSTNAME HOSTTYPE
  echo ${#HOME} # length of variable HOME
  11
  ```

- Command substitution

  Command substitution allows the output of a command to replace the command itself. It can be nested.

  ```shell
  $ $(pwd)
  /home/youwu/work/scripts
  $ $(ls $(pwd))
  script1.sh
  $ `pwd`
  /home/youwu/work/scripts
  $ `ls \`pwd\``
  script1.sh
  ```

- Arithmetic expansion

  Arithmetic expansion allows the evaluation of an arithmetic expression and the substitution of the result. The operators are roughly the same as in the C programming language.

  ```shell
  $ echo $((1*2+3*4))
  14
  $ VAR=1
  $ echo $[++VAR]
  2
  ```

- Process substitution

  Process substitution is supported on systems that support named pipes (FIFOs) or the `/dev/fd` method of naming open files.

### Aliases

An alias allows a string to be substituted for a word when it is used as the first word of a simple command. The shell maintains a list of aliases that may be set and unset with the **alias** and **unalias** built-in commands.

```shell
$ alias             # show the current aliases
alias ls='ls --color=auto'
$ alias ..='cd ..'  # create aliase
$ unalias ..        # remove aliase
```



## Regular expressions

A *regular expression* is a pattern that describes a set of strings. The fundamental building blocks are the regular expressions that match a single character.

### Regular expression metacharacters

| Operator | Effect                                                       |
| -------- | ------------------------------------------------------------ |
| .        | Matches any single character.                                |
| ?        | The preceding item is optional and will be matched, at most, once. |
| *        | The preceding item will be matched zero or more times.       |
| +        | The preceding item will be matched one or more times.        |
| {N}      | The preceding item is matched exactly N times.               |
| {N,}     | The preceding item is matched N or more times.               |
| {N,M}    | The preceding item is matched at least N times, but not more than M times. |
| -        | represents the range if it's not first or last in a list or the ending point of a range in a list. |
| ^        | Matches the empty string at the beginning of a line; also represents the characters not in the range of a list. |
| $        | Matches the empty string at the end of a line.               |
| \b       | Matches the empty string at the edge of a word.              |
| \B       | Matches the empty string provided it's not at the edge of a word. |
| \\<      | Match the empty string at the beginning of word.             |
| \\>      | Match the empty string at the end of word.                   |

Two regular expressions may be joined by the infix operator "|"; the resulting regular expression matches any string matching either subexpression.

In basic regular expressions the metacharacters "?", "+", "{", "|", "(", and ")" lose their special meaning; instead use the backslashed versions "\?", "\\+", "\\{", "\\|", "\\(", and "\\)".

### Example using grep

**grep** searches the input files for lines containing a match to a given pattern list. When it finds a match in a line, it copies the line to standard output (by default), or whatever other sort of output you have requested with options.

```shell
# displays the lines from /etc/passwd containing the string root.
grep root /etc/passwd
# displays the line numbers containing this search string.
grep -n root /etc/passwd
# checks which users are not using bash, ignoring the accounts with the nologin shell 
grep -v bash /etc/passwd | grep -v nologin
# counts the number of accounts that have /bin/false as the shell.
grep -c false /etc/passwd
# displays the lines from all the files in her home directory starting with ~/.bash, 
# excluding matches containing the string history
grep -i ps ~/.bash* | grep -v history
```

To work more powerfully, use **grep** with regular expressions.

```shell
# To see which accounts have no shell assigned whatsoever
grep :$ /etc/passwd
# To check that PATH is exported in ~/.bashrc
grep export ~/.bashrc | grep '\<PATH'
# To display information for the root partition, finding a string that is a separate
# word (enclosed by spaces)
grep -w / /etc/fstab
```

A *bracket expression* is a list of characters enclosed by "[" and "]". It matches any single character in that list; if the first character of the list is the caret, "^", then it matches any character NOT in the list. Within a bracket expression, a *range expression* consists of two characters separated by a hyphen.

```shell
[0123456789] 	# matches any single digit
[a-d]			# matches single character a,b,c,d
[^0-9]			# matches any characters that is not digit
```

Use the "." for a single character match.

```shell
# get a list of all five-character words starting with "c" and ending in "h"
grep '\<c...h\>' /usr/share/dict/words
# selects all words starting with "c" and ending in "h" from the system's dictionary
grep '\<c.*h\>' /usr/share/dict/words
# to display lines containing the literal dot character, use the -F option
grep . /usr/share/dict/words -F
# finding the asterisk character in /etc/profile
grep '*' /etc/profile
```

### Pattern matching using Bash features

Apart from **grep** and regular expressions, there's a good deal of pattern matching that you can do directly in the shell, without having to use an external program.

The asterisk (*) and the question mark (?) match any string or any single character. Quote these special characters to match them literally. Square braces can be used to match any enclosed character or range of characters.

```shell
ls *.h					# list all .h files
ls "*"					# list all files or directories include *
ls -ld [a-cx-z]*		# list all files starting with "a", "b", "c", "x", "y" or "z"
ls [!a]*				# list all files not starting with a
```

Character classes can be specified within the square braces, using the syntax **[:CLASS:]**, where CLASS is defined in the POSIX standard and has one of the values: `alnum`, `alpha`, `ascii`, `blank`, `cntrl`, `digit`, `graph`, `lower`, `print`, `punct`, `space`, `upper`, `word` or `xdigit`.

```shell
ls -ld [[:digit:]]*		# list all files composed of digit
ls -ld [[:upper:]]*		# list all files composed of upper characters
```

## The GNU sed stream editor

A Stream EDitor is used to perform basic transformations on text read from a file or a pipe. The result is sent to standard output.

The syntax for the **sed** command has no output file specification, but results can be saved to a file using output redirection. The editor does not modify the original input.

What distinguishes **sed** from other editors, such as **vi** and **ed**, is its ability to filter text that it gets from a pipeline feed. You do not need to interact with the editor while it is running; that is why **sed** is sometimes called a *batch editor*. This feature allows use of editing commands in scripts, greatly easing repetitive editing tasks. When facing replacement of text in a large number of files, **sed** is a great help.

### Sed commands

| Command | Result                                         |
| ------- | ---------------------------------------------- |
| a\      | Append text below current line.                |
| c\      | Change text in the current line with new text. |
| d       | Delete text.                                   |
| i\      | Insert text above current line.                |
| p       | Print text.                                    |
| r       | Read a file.                                   |
| s       | Search and replace text.                       |
| w       | Write to a file.                               |

### Interactive editing

Printing lines containing a pattern, use `p` to obtain the result:

```shell
# print the entire file, but the lines containing the search string are printed twice.
sed '/erors/p' example
# only print those lines matching our pattern
sed '/erors/p' example -n
# only print the lines starting with 'This'
sed -n '/^This.*errors.$/p' example
```

Deleting lines of input containing a pattern in print info, use `d` to exclude them:

```shell
# only want to see the lines not containing the search string
sed '/erors/d' example
```

Choosing the certain lines to print or exclude:

```shell
# to take out the lines 2-4
sed '2,4d' example
# to take out the lines from 3 to the end of the file
sed '3,$d' example
# prints the first line containing the pattern "a text", up to and including the next
# line containing the pattern "a line"
sed -n '/a text/,/This/p' example
```

 Find and replace the pattern:

```shell
# replace 'erors' with 'errors', only replace the first occurance of each line
sed 's/erors/errors/' example
# replace all 'erors' with 'erros'
sed 's/erors/errors/g' example
# To insert(replace) '> ' at the beginning of each line of a file
sed 's/^/> /' example
# To insert(replace) 'EOL' at the end of each line
sed 's/$/EOL/' example
```

Multiple find and replace commands are separated with individual `-e` options:

```shell
# replace all 'erors' with 'erros', and replace all 'last' with 'final'
sed -e 's/erors/errors/g' -e 's/last/final/g' example
```



##  The GNU awk programming language

Gawk is the GNU version of the commonly available UNIX **awk** program, another popular stream editor. Since the **awk** program is often just a link to **gawk**, we will refer to it as **awk**.

The basic function of **awk** is to search files for lines or other text units containing one or more patterns. When a line matches one of the patterns, special actions are performed on that line.

### The print program

The **print** command in **awk** outputs selected data from the input file.

When **awk** reads a line of a file, it divides the line in fields based on the specified *input field separator*, `FS`, which is an **awk** variable. This variable is predefined to be one or more spaces or tabs. The variables `$1`, `$2`, `$3`, ..., `$N` hold the values of the first, second, third until the last field of an input line. The variable `$0` (zero) holds the value of the entire line. 

````shell
# list 
$ ls -ldh
-rwxr-xr-x 1 youwu youwu 76 5月 13 22:13 script1.sh
# filter out the useful info
$ ls -ldh * | grep -v total | awk '{ print "Size is " $5 " bytes for " $9 }'
Size is 76 bytes for script1.sh
# print using commas
$ ls -ldh * | grep -v total | awk '{ print "Size is", $5, "bytes for", $9 }'
Size is 76 bytes for script1.sh
# search the /etc directory for files ending in ".conf" and starting with "a" or "x"
ls -l | awk '/\<[a|x].*\.conf$/ { print $9 }'
````

We can print message at the begin or end of the process:

```shell
ls -l | awk 'BEGIN { print "Files found:\n" } /\<[a|x].*\.conf$/ { print $9 }'
ls -l | awk '/\<[a|x].*\.conf$/ { print $9 } END { print "Over." }'
```

### Gawk variables

The **field separator**, which is either a single character or a regular expression, controls the way **awk** splits up an *input record* into fields. The default input field separator is one or more whitespaces or tabs. User can change its value in the **awk** program with the assignment operator **=**.

```shell
# use ':' to be FS
$ awk 'BEGIN { FS=":" } { print $1 "\t" $5 }' /etc/passwd
kelly	Kelly Smith
```

The output from an entire **print** statement is called an *output record*. Similar with `FS`, **output separator**, `OFS` can be used to split the output. Each **print** command results in one output record, and then outputs a string called the **output record separator**, `ORS`. The default value for this variable is "\n", a newline character.

```shell
# use ';' to be OFS, "\n-->\n" to be ORS
$ awk 'BEGIN { OFS=";" ; ORS="\n-->\n" } { print $1,$2}' test
record1;data1
-->
record2;data2
-->
```

The built-in `NR` holds the number of records that are processed. It is incremented after reading a new input line. You can use it at the end to count the total number of records, or in each output record:

```shell
$ cat processed.awk
BEGIN { OFS="-" ; ORS="\n--> done\n" }
{ print "Record number " NR ":\t" $1,$2 }
END { print "Number of records processed: " NR }
$ awk -f processed.awk test
Record number 1:        record1-data1
--> done
Record number 2:        record2-data2
--> done
Number of records processed: 2
--> done
```

Apart from the built-in variables, you can define your own. When **awk** encounters a reference to a variable which does not exist (which is not predefined), the variable is created and initialized to a null string. Variables can be a string or a numeric value.

Values can be assigned directly using the **=** operator, or you can use the current value of the variable in combination with other operators.

```shell
$ cat revenues
20021009        20021013        consultancy     BigComp         2500
20021015        20021020        training        EduComp         2000
20021112        20021123        appdev          SmartComp       10000
20021204        20021215        training        EduComp         5000
$ cat total.awk
{ total=total + $5 }
{ print "Send bill for " $5 " dollar to " $4 }
END { print "---------------------------------\nTotal revenue: " total }
$ awk -f total.awk test
Send bill for 2500 dollar to BigComp
Send bill for 2000 dollar to EduComp
Send bill for 10000 dollar to SmartComp
Send bill for 5000 dollar to EduComp
---------------------------------
Total revenue: 19500
```



## Conditional statements

### Introduction to if

The most compact syntax of the **if** command is:

```shell
if TEST-COMMANDS; then CONSEQUENT-COMMANDS; fi
```

The **TEST-COMMAND** list is executed, and if its return status is zero, the **CONSEQUENT-COMMANDS** list is executed. The return status is the exit status of the last command executed, or zero if no condition tested true.

#### Primary expression

The table below contains an overview of the some common "primaries" that make up the **TEST-COMMAND** command or list of commands. More details are described in [Introduction to if](<http://www.tldp.org/LDP/Bash-Beginners-Guide/html/sect_07_01.html>). 

| Primary                            | Meaning                                                      |
| ---------------------------------- | ------------------------------------------------------------ |
| [ -a `FILE` ] or [ -e `FILE` ] | True if `FILE` exists.                                       |
| [ -d `FILE` ]                    | True if `FILE` exists and is a directory.                    |
| [ -f `FILE` ]                    | True if `FILE` exists and is a regular file.                 |
| [ -s `FILE` ]                    | True if `FILE` exists and has a size greater than zero.      |
| [ -x `FILE` ]                    | True if `FILE` exists and is executable.                     |
| [ -N `FILE` ]                    | True if `FILE` exists and has been modified since it was last read. |
| [ `FILE1` -nt `FILE2` ]          | True if `FILE1` has been changed more recently than `FILE2`, <br />or if `FILE1` exists and `FILE2` does not. |
| [ `FILE1` -ot `FILE2` ]          | True if `FILE1` is older than `FILE2`, or is `FILE2` exists and<br /> `FILE1` does not. |
| [ -z `STRING` ]                      | True of the length if "STRING" is zero.                      |
| [ -n `STRING` ] or [ `STRING` ]        | True if the length of "STRING" is non-zero.                  |
| [ `STRING1` == `STRING2` ]             | True if the strings are equal.                               |
| [ `STRING1` != `STRING2` ]             | True if the strings are not equal.                           |
| [ `ARG1` `OP` `ARG2` ]                   | "OP" is one of `-eq`, `-ne`, `-lt`, `-le`, `-gt` or `-ge`. <br />Respectively. "ARG1" and "ARG2" are integers. |

#### Simple applications of **if**

```shell
# use the exit status of the previously executed command as condition
if [ $? -eq 0 ]; then CONSEQUENT-COMMANDS; fi
# use ! in condition
if ! grep $USER /etc/passwd; then CONSEQUENT-COMMANDS; fi
# use numerical comparisons
num=`wc -l work.txt`
if [ "$num" -gt "150" ]; then CONSEQUENT-COMMANDS; fi
# use comparing strings
if [ "$(whoami)" != 'root' ]; then CONSEQUENT-COMMANDS; fi
# use regular expressions
if [[ "$gender" == f* ]]; then CONSEQUENT-COMMANDS; fi
# use '&&' or '||' to shorten command
[ "$(whoami)" != 'root' ] && (CONSEQUENT-COMMANDS)
# use test to replace []
test "$(whoami)" != 'root' && (CONSEQUENT-COMMANDS)
```

Contrary to `[`, `[[` prevents word splitting of variable values and pathname expansion. It is a good habit to using quotes.

### More advanced if usage

The full form of the **if** statement:

```shell
if TEST-COMMANDS; then
    CONSEQUENT-COMMANDS;
elif MORE-TEST-COMMANDS; then
    MORE-CONSEQUENT-COMMANDS;
else 
    ALTERNATE-CONSEQUENT-COMMANDS;
fi
```

**If** statement can be nested.

```shell
if [ $[$year % 400] -eq "0" ]; then
  echo "This is a leap year.  February has 29 days."
elif [ $[$year % 4] -eq 0 ]; then
        if [ $[$year % 100] -ne 0 ]; then
          echo "This is a leap year, February has 29 days."
        else
          echo "This is not a leap year.  February has 28 days."
        fi
else
  echo "This is not a leap year.  February has 28 days."
fi
```

Use the positional parameters `$1`, `$2`, ..., `$N` for this purpose. `$#` refers to the number of command line arguments. `$0` refers to the name of the script.

```shell
if [ ! $# == 2 ]; then
  echo "Usage: $0 weight_in_kilos length_in_centimeters"
  exit
fi
```

**exit** terminates execution of the entire script. It takes an optional argument. This argument is the integer exit status code, which is passed back to the parent and stored in the `$?` variable. 0 for success, others for errors.

```shell
exit 0
```

### Using case statements

For the more complex conditionals, use the **case** syntax:

```shell
case EXPRESSION in 
  CASE1) COMMAND-LIST;; 
  CASE2) COMMAND-LIST;; 
  ... 
  CASEN) COMMAND-LIST;;
esac
```

Each case is an expression matching a pattern. The commands in the **COMMAND-LIST** for the first match are executed. The "|" symbol is used for separating multiple patterns, and the ")" operator terminates a pattern list. Each case plus its according commands are called a *clause*. Each clause must be terminated with ";;". Each **case** statement is ended with the **esac** statement.

```shell
case $space in
[1-6]*)
  Message="All is quiet."
  ;;
[7-8]*)
  Message="Start thinking about cleaning out some stuff.  There's a partition that is $space % full."
  ;;
9[1-8])
  Message="Better hurry with that new disk...  One partition is $space % full."
  ;;
99)
  Message="I'm drowning here!  There's a partition at $space %!"
  ;;
*)
  Message="I seem to be running with an nonexistent amount of disk space..."
  ;;
esac
```

### read

#### Using the read built-in command

The **read** built-in command is to catch user input. The syntax of the **read** command is as follows:

```shell
read [options] NAME1 NAME2 ... NAMEN
```

The following options are supported by the Bash **read** built-in:

| Option | Meaning                                                      |
| ------ | ------------------------------------------------------------ |
| -d     | The first character of `DELIM` is used to terminate the input line, rather than newline. |
| -e     | **readline** is used to obtain the line.                     |
| -n     | **read** returns after reading `NCHARS` characters rather than waiting for a complete line. |
| -r     | If this option is given, backslash does not act as an escape character. |
| -s     | Silent mode. If input is coming from a terminal, characters are not echoed. |
| -t     | Cause **read** to time out and return failure if fail to read a line within `TIMEOUT` seconds. |
| -u     | Read input from file descriptor `FD`.                        |

Example:

```shell
echo "Type the year that you want to check (4 digits), followed by [ENTER]:"
read year
```

### Redirection and file descriptors

Redirection can be used to change the script's input and output.

- Redirection "N>&M" or "N<&M" after a command has the effect of creating or updating the symbolic link `/proc/self/fd/N` with the same target as the symbolic link `/proc/self/fd/M`.
- The redirections "N> file" and "N< file" have the effect of creating or updating the symbolic link `/proc/self/fd/N` with the target file.
- File descriptor closure "N>&-" has the effect of deleting the symbolic link `/proc/self/fd/N`.

*stdin*, *stdout* and *stderr* are the best known file descriptors, with file descriptor numbers 0, 1 and 2. Redirect them to make scripts more flexible.

```shell
# standard error is copied to standard output, standard output to the destination file
ls -l * 2 >& 1 > /var/tmp/spoollist
```

The **exec** built-in command can be used to replace the shell of the current process or to alter the file descriptors of the current shell. For example, it can be used to assign a file descriptor to a file.

```shell
# for assigning file descriptor N to file for output, and
exec fdN> file
# for assigning file descriptor N to file for input.
exec fdN< file
```

The ***here* document** provides a way of instructing the shell to read input from the current source until a line containing only the search string is found (no trailing blanks). All of the lines read up to that point are then used as the standard input for a command.

```shell
# installs a package automatically，the script answers "y"
yum install $1 << CONFIRM
y
CONFIRM
```



## Repetitive task

### The for loop

This loop allows for specification of a list of values. A list of commands is executed for each value in the list. The syntax for this loop is:

```shell
for NAME [in LIST ]; do COMMANDS; done
```

If **[in LIST]** is not present, it is replaced with **in $@** and **for** executes the **COMMANDS** once for each positional parameter that is set.

The return status is the exit status of the last command that executes. If no commands are executed because `LIST` does not expand to any items, the return status is zero.

```shell
# using the result of ls coommand
for i in `ls *`; do 
	((count += 1));
done
# using the shell's globbing feature
for i in *; do
	((count += 1));
done
# using the array
list=( 1 2 3)
for i in ${list[*]}; do 
	((count += 1));
done
# using the arguments
for i; do
	echo i;
done
```

### The while loop

The **while** construct allows for repetitive execution of a list of commands, as long as the command controlling the **while** loop executes successfully (exit status of zero). The syntax is:

```shell
while CONTROL-COMMAND; do CONSEQUENT-COMMANDS; done
```

As soon as the **CONTROL-COMMAND** fails, the loop exits. In a script, the command following the **done** statement is executed.

The return status is the exit status of the last **CONSEQUENT-COMMANDS** command, or zero if none was executed.

### The until loop

The **until** loop is very similar to the **while** loop, except that the loop executes until the **TEST-COMMAND** executes successfully. As long as this command fails, the loop continues. The syntax is the same as for the **while** loop:

```shell
until TEST-COMMAND; do CONSEQUENT-COMMANDS; done
```

The return status is the exit status of the last command executed in the **CONSEQUENT-COMMANDS** list, or zero if none was executed. **TEST-COMMAND** can, again, be any command that can exit with a success or failure status, and **CONSEQUENT-COMMANDS** can be any UNIX command, script or shell construct.

### Break and continue

The **break** statement is used to exit the current loop before its normal ending. 

The **continue** statement resumes iteration of an enclosing **for**, **while**, **until** or **select** loop.

### Making menus with the select built-in

The **select** construct allows easy menu generation. The syntax is quite similar to that of the **for** loop:

```shell
select WORD [in LIST]; do RESPECTIVE-COMMANDS; done
```

`LIST` is expanded, generating a list of items. The expansion is printed to standard error; each item is preceded by a **number**. If **in LIST** is not present, the positional parameters are printed, as if **in $@** would have been specified. `LIST` is only printed once.

Upon printing all the items, the `PS3` prompt is printed and one line from standard input is read. If this line consists of a number corresponding to one of the items, the value of `WORD` is set to the name of that item. If the line is empty, the items and the `PS3` prompt are displayed again. If an *EOF* (End Of File) character is read, the loop exits. Since most users don't have a clue which key combination is used for the EOF sequence, it is more user-friendly to have a **break** command as one of the items. Any other value of the read line will set `WORD` to be a null string.

The read line is saved in the `REPLY` variable.

The **RESPECTIVE-COMMANDS** are executed after each selection until the number representing the **break** is read. This exits the loop.

```shell
$ cat script3.sh
select i in "aa" "bb" "cc"; do
    case $i in 
        a)
            echo "Your choice is a"
            PS3="Your choice: "
        ;;
        b)
            echo "Your choice is $REPLY"
        ;;
        c)
            echo "Your choice is $i";
            break;
        ;;
        *)
            echo "Wrong choice! exit!"
        ;;
    esac
done
$ ./script3.sh
1) aa
2) bb
3) cc
#? 1
Your choice is a
Your choice: 2
Your choice is 2
Your choice: 3
```



## More On Variables

### Types of variables

Using a **declare** statement, we can limit the value assignment to variables. The syntax for **declare** is the following:

```shell
declare OPTION(s) VARIABLE=value
```

The following options are used to determine the type of data the variable can hold and to assign it attributes:

| Option | Meaning                                                      |
| ------ | ------------------------------------------------------------ |
| `-a`   | Variable is an array.                                        |
| `-f`   | Use function names only.                                     |
| `-i`   | The variable is to be treated as an integer; arithmetic evaluation is performed when the variable is assigned a value |
| `-p`   | Display the attributes and values of each variable. When `-p` is used, additional options are ignored. |
| `-r`   | Make variables read-only. These variables cannot then be assigned values by subsequent assignment statements, nor can they be unset. |
| `-t`   | Give each variable the *trace* attribute.                    |
| `-x`   | Mark each variable for export to subsequent commands via the environment. |

Example:

```shell
$ declare -i VARIABLE=12
$ VARIABLE=string
$ echo $VARIABLE
0
```

### Array Variables

An array is a variable containing multiple values. Arrays are zero-based: the first element is indexed with the number 0.

```shell
# Indirect declaration is done using the following syntax to declare a variable:
ARRAYNAME[INDEXNR]=value
# Explicit declaration of an array is done using the **declare** built-in:
declare -a ARRAYNAME
# Array variables may also be created using compound assignments in this format:
ARRAYNAME=(value1 value2 ... valueN)
```

In order to refer to the content of an item in an array, use curly braces. Referring to the content of a member variable of an array without providing an index number is the same as referring to the content of the first element, the one referenced with index number zero.

```shell
$ ARRAY=(one two three)
$ echo ${ARRAY[*]}
one two three
$ echo $ARRAY[*]
one[*]
$ echo ${ARRAY[2]}
three
$ ARRAY[3]=four
$ echo ${ARRAY[*]}
one two three four
```

The **unset** built-in is used to destroy arrays or member variables of an array:

```shell
unset ARRAY[1]  # remove the element of index 1
unset ARRAY     # remove the whole array 
```

### Operations on variables

```shell
# calculate the length of variable
$ echo $SHELL, ${SHELL}
/bin/bash, 9
# calculate the size of array
$ ARRAY=(one two three); echo ${#ARRAY}
3
# use a default value if variable is not defined
$ echo {TEST:-test}
# assign the variable with a default
$ echo {TEST:=test}
# substring the varible
$ export STR="helloworld"; echo ${STR:4}, ${STR:5:5}
oworld, world
# remove words begin with the shortest matched pattern or longest matched pattern
$ echo ${ARRAY[*]}; echo ${ARRAY[*]#t*}; echo ${ARRAY[*]##t*}
one two one three one four
one wo one hree on four
one one one four
# remove words end with the shortest matched pattern or longest matched pattern
$ echo ${ARRAY[*]}; echo ${ARRAY[*]%*e}; echo ${ARRAY[*]%%*e}
one two one three one four
on two on thre on four
two four
# replace the pattern with string
$ echo ${STR}, ${STR/world/ xxs}
helloworld, hello xxs
```



## Functions

Shell functions are a way to group commands for later execution, using a single name for this group, or routine. When calling on a function as a simple command name, the list of commands associated with that function name is executed. A function is executed within the shell in which it has been declared: no new process is created to interpret the commands. 

There are two ways to declare a function"

```shell
function FUNCTION { COMMANDS; }
FUNCTION() { COMMANDS; }
```

**NOTE**. The curly braces must be separated from the body by spaces, otherwise they are interpreted in the wrong way. The body of a function should end in a semicolon or a newline.

Function can accept parameters. The function use the same way with getting script arguments to get the function arguments.

```shell
$ cat testFuncPara.sh
echo "The script parameter is $1"
function test() {
	echo "The function parameter is $1"
}
test "foo"
$ ./testFuncPara "script"
The script parameter is script
The function parameter is foo
```

On some Linux systems, for instance, you will find the /etc/rc.d/init.d/functions definition file, which is sourced in all init scripts. Using this method, common tasks such as checking if a process runs, starting or stopping a daemon and so on, only have to be written once, in a general way. 

You could make your own /etc/functions file that contains all functions that you use regularly on your system, in different scripts. Just put the line

```shell
. /etc/functions
```

somewhere at the start of the script and you can recycle functions.



## Catching signals

### Signals

In the absence of any traps, an interactive Bash shell ignores `SIGTERM` and `SIGQUIT`. `SIGINT` is caught and handled, and if job control is active, `SIGTTIN`, `SIGTTOU` and `SIGTSTP` are also ignored. `SIGHUP` by default exits a shell. An interactive shell will send a SIGHUP to all jobs, running or stopped. `SIGKILL` and `SIGSTOP` can not be caught, blocked or ignored, they kill the process directly.

When killing a process or series of processes, it is common sense to start trying with the least dangerous signal, `SIGTERM`. That way, programs that care about an orderly shutdown get the chance to follow the procedures that they have been designed to execute when getting the `SIGTERM` signal, such as cleaning up and closing open files. If you send a `SIGKILL` to a process, you remove any chance for the process to do a tidy cleanup and shutdown, which might have unfortunate consequences.

### Traps

There might be situations when you don't want users of your scripts to exit untimely using keyboard abort sequences, for example because input has to be provided or cleanup has to be done. The trap statement catches these sequences and can be programmed to execute a list of commands upon catching those signals.

The syntax for the trap statement is straightforward:

```shell
trap [COMMANDS] [SIGNALS]
```

If a signal is 0 or EXIT, the COMMANDS are executed when the shell exits. If one of the signals is DEBUG, the list of COMMANDS is executed after every simple command. A signal may also be specified as ERR; in that case COMMANDS are executed each time a simple command exits with a non-zero status. Note that these commands will not be executed when the non-zero exit status comes from part of an if statement, or from a while or until loop. Neither will they be executed if a logical AND (&&) or OR (||) result in a non-zero exit code, or when a command's return status is inverted using the ! operator.

```shell
trap "echo Booh! SIGINT SIGTERM"
echo "pid is $$"
while : do     # same as while true
	sleep 60;
done
```

When Bash receives a signal for which a trap has been set while waiting for a command to complete, the trap will not be executed until the command completes. When Bash is waiting for an asynchronous command via the wait built-in, the reception of a signal for which a trap has been set will cause the wait built-in to return immediately with an exit status greater than 128, immediately after which the trap is executed.



## Demo

统计某工作目录及其子目录下.c文件一共有多少行：

```shell
find [dir] -name "*.c" | xargs cat | grep -v "^$" | wc -l
```

统计某文件中出现最多的10个单词的次数，格式为一行一个单词：

```shell
cat [file] | awk '{words[$0]++} END {for(word in words) print word words[word]"}' | sort -k2r | head -10
# or
cat [file] | awk '{print $1}' | sort | uniq -c | sort -k1r | head -10
```

统计某文件中出现最多的10个单词的次数，正常文本：

```shell
cat [file] | tr -cs [:alnum:] "\n" | sort | uniq -c | sort -k1r | head -10
```



## 参考文献

1. [Bash Guide for Beginners](http://www.tldp.org/LDP/Bash-Beginners-Guide/html/index.html)
2. [linux bash Shell特殊变量：Shell $0, $#, $*, $@, $?, $$和命令行参数](https://www.cnblogs.com/chjbbs/p/6393805.html)
3. [bash八大扩展一网打尽](https://www.cnblogs.com/welkinwalker/archive/2013/02/12/2910288.html)
4. [shell脚本统计单词频率、出现次数最多的n个单词](https://www.cnblogs.com/oldtrafford/p/3723277.html)
5. [统计文件中出现的单词次数](https://www.cnblogs.com/kevingrace/p/8670623.html)
6. [Linux tr命令](<https://blog.csdn.net/huangyimo/article/details/79134000>)

