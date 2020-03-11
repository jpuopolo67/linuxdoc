# linuxdoc
A place to capture Linux learning

# Essential Commands
*Note* most commands accept --help

* ^L - clear the screen
* ^R - search in console command history
* whoami - displays current user
* who am i - displays current user plus addition info
* hostname - information about the current host
* uname - prints system info
* man <section #1-9> help - man pages
* man -k <keyword> or apropos: sections 1, 5, 8 most important in general
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
* sudo -s (AWS EC2 instance - activates root shell)
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
* chvt - change virtual terminal
* who - list of users logged into the system with tty connections
* ssh - login into a remote computer. Note ssh -X will enable graphical windows if
you have an X Server on your client. 
* ssh-keygen - generates public/private key pair
* ssh-copy-id - copies keys to remote server 
* scp - securely copy a file, etc. to a remote server over ssh
* tee - combines redirection and piping, i.e., write out + send as input to another command
* env - display environment variables
* VARNAME=VARVALUE to define a shell variable
* export VARNAME makes VARNAME available in subshells
* alias - define aliases
* chown - change owner
* chgrp - change group
* chmod - change permissions/mode
* suid, sgid, sticky - special permissions - run as a given user or group owner
* umask - define a mask that will be subtracted from the default permissions, set in /etc/profile
* cfdisk - display or manipulate a partition table
* fdisk - manipulate disk partition table
* gdisk - interactive GUID partition table (GPT) manipulator 
* lsblk - list block devices
* partprobe - update kernel after changing partition table
* mkfs - make file system (various types available, e.g., xfs is default on many distributions)
* mount - attach a partition and file system to a directory
* umount - unmount a file system
* lsof - list open files/what process is using a file
* findmnt - find out what is mounted and where
* ip - manipulate IP information
* dhclient - run DHCP client/obtain IP address
* ping - send ICMP packet
* netstat - print network connections, routing tables, interface statistics, masquerade connections, and multicast memberships
* ss - more modern alternative to netstat
* nmap - network exploration tool and security & port scanner
* dig - DNS lookup utility
* hostname - show or set system's hostname
* hostnamectl - control the system hostname
* 
  
## Key Directories
* /usr/share/doc - doc for installed packages
* /var - system-created files, e.g., /var/log - system log files
* /bin -> /usr/bin, /sbin -> root command/system binaries
* /usr - contaqins all of the binaries etc. that computer uses
* /dev - device files - provide access to hardware
* /etc - configuration file - mostly text
* /opt - application file, e.g., databases
* /proc - running processes
* /dev/zero - "file" that produces zero bytes 

## Interesting Command Examples
* ip a
* ip route show
* ip a a dev eth0 1.2.3.4/8
* cat /etc/resolv.conf
* mount | grep '^/dev'
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
* grep '\<alex\>' namefile
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
* su - amy
* sudo visudo (editor for sudo configuration)
* sort < /etc/passwd
* sort < /etc/passwd > outfile
* ls > myfile
* echo "more text" >> myfile
* grep -R root /proc 2>/dev/null
* ps aux | tee psfile | grep ssh
* history -c, history -w 
* chmod g+s /data/account - sets groupid for directory /data/account
* touch file{a..z} - create a range of files: filea, fileb, ..., filez

## Redirection
* Standard input (0): <
* Standard output (1): >, >>
* Standard error (2): 2>, e.g., 2>/dev/null
* &>: redirect both stdout and stderr

## Important Ideas
* All the work on the machine is ultimately done by the kernel
* "Kernel land" is the land of core os, drivers and hardware
* "User land" is where user processes live
* User "root" lives in kernel land - so has no restrictions
* To cross from "user land" or "kernel land", user program make system library calls
* A shell is an interface into the OS
* Linux is very file-oriented - "everything is a file"
* Files are associated with one and only one *inode* (file metadata/admin data)
* Hard links point directly to inodes
* Symbolic links point to hard links, not directly to inodes
* To prevent the shell from interpreting wildcards before a command can interpret them, use '*'
* User ownership > group ownwerhip and Linux uses short-circuit evaluation on permissions
* Write permission to a **directory** enables deletion of files - even if you don't own the file!
* Sticky bit enforces that the owner of the directory or file is only allowed to delete a file
* VFAT is the only filesystem compatible among Windows, Linux and MacOS
