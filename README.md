# linuxdoc
A place to capture Linux learning

# Essential Commands
*Note* most commands accept --help

* ^L - clear the screen
* whoami - displays current user
* hostname - information about the current host
* uname - prints system info
* man <section #1-9> help - man pages
  man -k <keyword> or apropos
  sections 1, 5, 8 most important in general
* file - information about a file
* xxd - hex viewer
* date - see date
* cal - see calendar
* passwd - work with passwords
* touch - create empty file/update metadata
* last - shows last logins
* less - text viewer/pager
* su - switch user (su - = open login shell), e.g., su - to switch to root on centos (redhat)
* sudo -i (ubuntu)
* sudo <cmd> - run <cmd> as root
* wc - word/line count
* grep - filtering utility
* mandb - refresh man pages
* pinfo - a documentation system like man
* pwd - print working directory
* cd - change directory
* tr - translate characters
* ls - list files
* mount - attach storage to a file system directory
* cp - copy files
* mv - move or rename files
* mkdir - make a directory (my alias md does mkdir -p to make a path)
* rm - remove files and directoies
* ln - make a hard link (directly to inode) or symbolic link (to hard link)
* cd - change directory 
* !<#> - repeate commnad # from bash history
* history - get a list of past shell commands
* find - find files and directories by name, size, owner, etc.
* time <command> - times the given shell command
* xargs - accepts pipe input and works on it line-by-line (element by element)
* tar - create an archive, e.g., tar -cvf, tar -xvf, tar -tvf 
* gzip - most common compression utility
* dd - copy block devices
* tree - display directories, subdirectories and files in a clear manner
* head, tail - see top or bottom of file
* cat, tac - display or concat files, tac does it in reverse
* ps - show processes
* egrep - "grep" that can use extended regular expression
* cut - filter output from a text file or stream
* sort - sort files or streams, often used in pipes
* tr - translate characters
* awk - search for specific patterns
* sed - powerful stream editor

## Key Directories
* /usr/share/doc - doc for installed packages
* /var - system-created files, e.g., /var/log - system log files
* /bin -> /usr/bin, /sbin -> root command/system binaries
* /usr - contains all of the binaries etc. that computer uses
* /dev - device files - provide access to hardware
* /etc - configuration file - mostly text
* /opt - application file, e.g., databases
* /proc - running processes
* /dev/zero - "file" that produces zero bytes 

## Interesting Command Examples
* uname -a | cut -d' ' -f1,2,3,4,5,6,7,8,9,10,11,12 | tr ' ' '\n' 
* uname -a | tr ' ' '\n' 
* find ./ -name "\*.class" 
* find ./ -name "\*.class" -exec cp {} tmp/ \; 
* find /etc -exec grep -l amy {} \; -exec cp {} /root/amy \;
* find /etc/ -name '\*' -type f | xargs grep "127.0.0.1" 2>/dev/null
* man -k user | grep 8
* grep amy /etc/* 
* grep amy /etc/* amy 2>/dev/null
* grep -i hello demofile
* ps aux | grep ssh | -v grep
* grep -R root *
* grep -Rl root *
* grep -A3 amy /etc/passwd
* grep ^abc regfile
* grep '^abc' regfile
* grep 'abc$' regfile
* egrep 'ab{2}c' regfile
* egrep 'a[bB]c' regfile
* egrep '(123)' regfile
* egrep '(123){2}' regfile
* cd - (move to previous directory)
* dd if=/dev/zero of=big_zero_file bs=1M count=1024
* tail -f /var/log/messages
* cut -d : -f 1 /etc/passwd | sort
* echo hello | tr [:lower:] [:upper:]
* sed -n 5p /etc/passwd
* sed -i s/how/HOW/g myfile
* sed -i -e '2d' myfile
* awk -F : '{ print $4 }' /etc/passwd
* awk -F : '{ print $4 }' /etc/passwd | sort -n
* awk -F : '/amy/ { print $4 }' /etc/passwd 
* >> (bash redirection)
* 2> (redirect standard error), e.g., 2>/dev/null


## Important Ideas
* All the work is done by the kernel
* Linux is very file-oriented - "everything is a file"
* Files are associated with one and only one *inode* (file metadata/admin data)
* Hard links point directly to inodes
* Symbolic links point to hard links, not directly to inodes
* To prevent the shell from interpreting wildcards before a command can interpret them, use '*'
