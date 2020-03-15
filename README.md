# linuxdoc
A place to capture Linux learning

## Essential Commands

### Console Commands
* ^l - clear the screen
* ^r - search in console command history
* ^a - go to beginning of command line
* ^e - go to end of command line
* ^u - clear command line
* !<#> - run command <#> from history

### Help & Doc
* For shell builtins, use _help_ <builtin> vs. --help or _man_!
* Most commands accept __--help__
* mandb - refresh man pages
* man man
* man <section #1-9> help - man pages
* man -k <keyword> or apropos: sections 1, 5, 8 most important in general
* manpath - tells us where the man pages are stored
* type <command> - tells us which type a command is
* whereis - locate the binary, source, and manual page files for a command
* which - shows the full path of (shell) commandsq
* whatis - display manual page descriptions
* pinfo - a documentation system like man
* locate - builds a DB of the file system and queries that
* updatedb - builds the DB used by locate (see /etc/updatedb.conf)

### User-Oriented
* whoami - displays current user
* who am i - displays current user plus addition info
* w - display who is logged in and what they are doing
* id - get user identity
* passwd - work with passwords
* last - shows last logins/login histories
* su - switch user (su - = open login shell), e.g., su - to switch to root on centos (redhat)
* sudo -i (ubuntu) or sudo -s (AWS EC2 instance - activates root shell)
* sudo <cmd> - run <cmd> as root
* visudo - edit sudoers file

### System-Oriented
* hostname - information about the current host
* uname - prints system info
* lsmod - display status of modules in the kernel
* modprobe - add or remove a module from the kernel
* rmmod - remove a module from the kernel
* lspci - shows PCI devices connected to the system
* dmesg - print or control the kernel ring buffer
* poweroff - power system off
* shutdown - shut down the system
* wall - send a message to everybody's terminal
* systemctl - interface into systemd (documented further down in this file as well)
	* init and telinit are older commands (for SysV) that adjust run levels
* cloud-init - enables initialization of Linux VMs (including AWS, Azure, etc.)

### Shell-Oriented
* time <command> - times the given shell command
* history - get a list of past shell commands
* xargs - accepts pipe input and works on it line-by-line (element by element)
* chvt - change virtual terminal
* env - display environment variables
* VARNAME=VARVALUE to define a shell variable
* export VARNAME makes VARNAME available in subshells
* echo $VARNAME - display value of shell variable $VARNAME
* set/unset - set and unset shell options
* alias - define aliases
* ulimit - can set system/shell limits
* source <sh> - execute a script without starting another shell
	* often used in .bash\_profile to run ./bashrc
* screen - manage multiple screens
* tmux - terminal multi-plexer (like _screen_)
* ^Z - suspend a process (can be resumed via fg or bg)
* #! - she-bang, e.g., !#/bin/bash
* $? - return value from most recent command
* &&, || - "and", "or" - enable us to chain commands
	* ping -c1 google.com && echo "alive!" || echo "dead"
	* ping -c1 googledkhfd.com && echo "alive!" || echo "dead"
* ; - separate multiple commands on the same line
#### Redirection
* Standard input (0): <
* Standard output (1): >, >>
* Standard error (2): 2>, e.g., 2>/dev/null
* & - copies to another file descriptor
* 2>&1 - copies standard error to standard output
* &>: redirect both stdout and stderr
* | - pipe - take output of one command as input to another
* xargs - build and execute command lines from standard input
* tee - send output to stdout and to another stream
	
### Directories & Files
#### Directories
* pwd - print working directory
* ~ - refers to logged-in user's home directory
* mkdir - make a directory (-p option for hierarchy)
* cd - change directory
* rmdir - remove directory
* ln - make a hard link (directly to inode) or symbolic link (to hard link)
* ls - list files in directory and subdirectories
* tree - display directories, subdirectories and files in a clear manner

#### Files
* file - information about a file
* cat, tac - display or concat files, tac does it in reverse
* less - text viewer/pager
* head, tail - show beginning/end of a file
* touch - create empty file/update metadata
* cp - copy files
* mv - move or rename files
* rm - remove files and directories 
* stat - displays information about a file or file system

#### File & Text Processing
* wc - word/line count
* cut - remove sections from each line of files
* xxd - hex viewer
* tr - translate characters
* fmt - simple text formatter
* join - join lines of two files on a common field
* paste - merge lines of files
* nl - number lines of files
* od - octal (and other) dumper
* pr - convert text files for printing
* sort - sort files or streams, often used in pipes
* uniq - report or omit repeated lines in a file 
* split - split a file into pieces
* expand, unexpand - turns tabs->spaces and vice versa
* gzip - most common compression utility
* find - find files and directories by name, size, owner, etc.
* grep - search and filter
* egrep - "grep" that can use extended regular expression
* awk - text processing, search for specific patterns
* sed - powerful command-line stream editor
* md5sum - calc MD5 sum of a set of bytes (considered obsolete in 2020)
* sha256sum - calc SHA-256 (currently recommended hash function)


### Process Management
* ps - show processes, often run as 'pas aux'
* fuser - show which processes use the named files, sockets, or filesystems 
* top - display processes and resource consumption
* jobs - processes associate with a specific shell
* fg - run process in foreground (from background)
* bg - moves a process to the background (use ^Z to suspend)
* nice - adjust process priority when starting a process (-20=higheset priroty -> 19=lowest)
* renice - change priority of running process
* kill - kill or send signal to a process
* killall - kill all processes with a given name
* ^Z - suspend a command (resume via fg and bg)
* nohup - run command but do not display output on terminal
	* often combined with & (run process in background)
* free - display memory stats 
* watch - watch a command on a period

### Disks & Storage
* File systems organize the disk and prove facilites for directories, files, file naming, 
journaling, etc. Linux supports a variety of file systems, e.g.,ext4, xfs, etc.
* mount - show mounts or attach storage to a file system directory
* umount - unmount a file system
* /etc/fstab is a file that contains info about file system to mount on boot
* systemd/systemctl can also mount partitions (see mount targets)
* mkswap - format a partition as swap space
* swapon - tell Linux that it can use the swap space from mkswap
* tar - create an archive, e.g., tar -cvf, tar -xvf, tar -tvf 
* dd - copy block devices
* cfdisk - display or manipulate a partition table
* fdisk - manipulate disk partition table
* gdisk - interactive GUID partition table (GPT) manipulator 
* lsblk - list block devices
* partprobe - update kernel after changing partition table
* mkfs - make file system (various types available, e.g., xfs is default on many distributions)
* lsof - list open files/what process is using a file
* findmnt - find out what is mounted and where
* df - display free disk space
* du - display disk usage stats
* fsck - check file system integrity and and fix issues (wrapper that maps to file system-specific commands)
* tune2fs - adjust tunable filesystem parameters on ext2/ext3/ext4 filesystems
* xfs\_repair\ - checks and repairs XFS file systems
* xfs\_fsr\ - defragments XFS file systems
* xfs\_db\ - examine or debug an XFS file system
* blkid - lists all file system with UUIDs
	* /etc/fstab shows the UUIDs for mounts as well
* quotacheck - check disk quotas (see quota package)
* edquota - edit quotas for a user
* quotaon - enables quotas on the system
* quota - report quotas, etc.
* repquota - get a summarized quota report
* lvm - logical volume manager - split disks into smaller sets of pools
	* volume group - group of hard disks
	* physical extents - hard disk divisions (pieces)
	* logical volumes are made up of 1 or more extents
* MBR and GPT are different partition schemes
	* MBR is older
	* GPT is newer and supports much larger disk, files, file names, etc. 

### Network & Connectivity
* host - DNS lookup utility
* hostname - show or set system's hostname
* hostnamectl - control the system hostname
* ip - manipulate IP information, e.g., ip addr, ip link
	* note: ifconfig is OBSOLETE and shouldn't be used anymore
* route - show / manipulate the IP routing table
* nslookup - query Internet name servers interactively
* dig - DNS lookup utility with advanced features
* dhclient - run DHCP client/obtain IP address
* ping - send ICMP packet - also assess latency
* netstat - print network connections, routing tables, interface statistics, etc.
* ss - modern alternative to netstat
* traceroute - print the route packets trace to network host
* nmap - network exploration tool and security & port scanner
* ssh - login into a remote computer. Note ssh -X will enable graphical windows if you have an X Server on your client. 
* ssh-keygen - generates public/private key pair
* ssh-copy-id - copies ssh keys to remote server 
* scp - securely copy a file, etc. to a remote server over ssh
* nmcli - network manager CLI (was not installed in AWS Linux2 AMI)
* ifup, ifdown - bring interface up/down
* netcat - read and write TCP/UDP traffic over a network
* tcpd - monitors TCP traffic, e.g., telnet, FTP, RSH, finger, etc. as a front door
* systemd sockets
	* sockets enable processes to share data, even over a network
	* described as systemd units in /lib/systemd/system
	

### Accounts & Permission Management
* useradd, usermod, userdel - CRUD users
* adduser - uses "useradd" and provides nice features
* passwd - manage users' passwords
* chage - change password expiry information
* id - get user identity
* groupadd, groupmod, groupdel - add, modify, delete groups
* addgroup - uses groupadd and provides nice features
* getent - get info from administrative databases
* chown - change owner of directory or file
* chgrp - change group of directory or file
* chmod - change permissions/mode of directory or file
* suid, sgid, sticky - special permissions - run as a given user or group owner
* umask - define a mask that will be subtracted from the default permissions, set in /etc/profile
	* in other words, umask suppresses what would otherwise be a default
* vipw, vigr - editing tools for editing the password/shadow files and group files securely
* loginctl - performs session management

### Date, Time & I8N
* date - show the current date and time
* cal - display a calendar
* tzselect - selects a timezone (see TZ environment variable)
* hwclock - query or set hardware clock - influences the system clock, of course
* timedatectl - control system time and date and sync with NTP servers
* ntpdate - set the date and time via ntp (network time protocol)
* chronyc sources - ntp server info (stratum 1=atomic clock -> 16=error)
	* chronyc is the client to the chrony service that is a robust implementation of NTP
* locale - list current locale and what's available on the system (LC\_ALL overrides all other locale-
related env variables)
* iconv - convert text from one character encoding to another 

### System Management with _systemd_
* Manages everything
* Kernel starts systemd -> starts all services
* Event-driven (reacts)
* Systemd manages items called "units"
* Targets are groups of units that describe an end-state that we want Linux to be in
	* Via targets, we can get the machine in single-user mode, recovery mode, etc.
	* See _systemctl isolate_
* /usr/lib/systemd/system
* systemctl <command> - control commands and services
	* systemctl service <service>
	* systemctl list-unit-files
	* etc.

### Package & Library Management
*  A package is a tar ball with a script to copy files to the right location + a DB to keep
track of what is installed
* Packages use dependencies to get other software that they need
* Packages are signed for verification and validation, e.g., with GPG keys
* rpm - package manager for RedHat distros. Does not fetch dependencies! _Software managers_ used to solve
the dependencies problem, e.g., _yum_
* rpm -cq <package> provides some useful information about a given package
* rpm -qp <package> provides other useful information about a package
* ldd - shows libs used by a given program
* ldconfig - configure library linker
* yum - RedHat software manager, e.g., _yum install_, _yum search_, _yum remove_
* yum provides - helps find the right package to use
* yum repolist - shows the repos available and the total number of packages available
* yum list installed - list all installed packages
* yum update - update the system
* yum groups list - list package groups
* yum history, yum history undo
* apt - like yum on Ubuntu

### Scheduling Tasks
* cron - uses crond daemon
* crontab -e - edit cron tasks (see /etc/crontab)
* anacron - runs jobs periodically (like cron) but _doesn't assume system is running_
* at - run a job once at a given time
* atq - display jobs in the _at_ queue
* atrm - remove a job from the _at_ queue
* batch - run queued jobs for later execution, based on system load
* systemd timers - more modern solution than cron
	* end in .timer 
	* unit must be enabled
	* systemctl list-timers
	* see /lib/systemd/system
* systemd-run - run programs in transient scope or service or timer units

### Logging & Log Files
* syslog - legacy service/message logging standard (service is syslogd)
* rsyslog - more modern version of syslog logging (service is rsyslogd)
	* implements an interface for all applications to log
	* can be configured to receive logs from systemd-journald
* systemd-journald - systemd-integrated log service
* systemd-cat - manully send log message to systemd-journal
* journalctl - client interface to systemd-journald - query and display journal
	* all the important messages from the applications that systemd manages
* logger - log messages to /var/log/messages
* logrotate ‐ rotates, compresses, and mails system logs

### Printing
* CUPS - Common UNIX Printing System (current printing standard)
	* install cups and cups-bsd
	* CUPS server provides Web-based admin
* lpq - list jobs on the print queue
* cupsdisable - disables printer (jobs still queued up - good for mainteance)
* cupenable - enables printer

### Misc Security
* nologin - politely refuse a login
* xinetd - monitors network traffic and runs applications in response


## Key Directories & System Files
* / - root of the file system
* /etc - system and command configuration files - mostly text
* /usr - where user binaries are stored
* /home - user home directories
* /boot - stores the boot loader and all boot images
* /var - system-created files, e.g., /var/log - system log files
* /tmp - unique storage area available to all users
* /dev - device files - provide access to hardware
* /proc - running processes
* /sys - virtual file system containing information about kernel subsystems
* /usr/share/doc - doc for installed packages
* /bin -> /usr/bin, /sbin -> root command/system binaries
* /etc/udev - configures hardware and provide rules for hardware events
* /opt - application files, e.g., databases
* /dev/zero - "file" that produces zero bytes 
* /dev/null - swallows unwanted out (byte abyss)
* /etc/crontab - cron configuration file (older, see systemd timers instead)
* /etc/anacrontab - anacron configuration file
* /etc/at.* - various at configuration/permission files
* /etc/services - services and network configurations for them/with names
* /etc/ld.so.conf - where shared libs are listed
* /usr/local/lib - shared libs directory
* /etc/fstab is a file that contains info about file system to mount on boot
* /etc/shadow - file that stores encrypted passwords for users
* /etc/group - group info - can give a group a password
* /etc/skel - the template directory/files that a new user gets when he/she created
* /etc/bash.bashrc
* /etc/profile
* ~/.bash\_profile, ~/.bashrc, ~/.profile
* ~/.bash\_login, ~/.bash\_logout (execute on these actions)
* /lib/systemd/system - for systemd
* /etc/timezone - tells the system where we are in the world
* /etc/localtime - configures what applications use to show dates and times
* /etc/adjtime - shows how hw clock is being stored/represented, e.g., LOCAL vs UTC time
* /etc/rsyslog.d - rsyslogd configuration file
* /var/log/* - system log files for various facilities
* /etc/logrotate.conf - logrotate configuration file
* /etc/systemd/journald.conf - journalctl configuration file
* /etc/aliases - email aliases and distribution list (see newaliases command)
* .forward - used to forward user's email to another user
* /etc/hostname - defines the computer's host name
* /etc/hosts - local version of DNS that helps with routing, e.g., if DNS were down or malfunctioning
* /etc/nsswitch.conf - tells the system how to look up host info - in _order_
* /etc/resolv.conf - DNS resolvers (do not edit manaully)
* /etc/dhcp/dhclient.conf - edit to update resolv.conf (DHCP will update for you)
* /etc/hosts.allow/deny - control access from client applications/protocols
* /etc/nologin - control nologin configuration
* /etc/xinetd.d/ - xinetd config
* /etc/ssh/ssh\_config - configs outbound SSH sessions you make from this machine
* /etc/ssh/sshd\_config - configs inbound SSH sessions   

## Command Examples
* sudo find / -perm /u=s,g=s - search for any file with suid or sgid set
* sudo route add default gw 192.168.0.254
* ntpdate pool.ntp.org
* set -o noclobber -- changes how file over-writing works
* set -o xtrace -- shows how the shell interprets a given command
* ps auxf -- the _f_ shows a nice tree structure of parent-child processes
* cat /proc/self/mount -- show mounted file systems
* sudo du -h --max-depth=1 -- display summary of storage used by all directories below current
* screen <command> - runs command in a screen session
* ls >x 2>&1 - stdout is redirected to x and standard error is copied to standard stdout
* ls >x 2>&1 >y - binds stderror to x and standard output to y
* dd if=/dev/sda of=bootloader.bak bs=446 count=1 -- takes a copy of the bootloader from primary hard drive
* tail -f /var/log/messages
* journalctl --dmesg
* ip a
* ip route show
* ip a a dev eth0 1.2.3.4/8
* cat /etc/resolv.conf
* ss -tuna
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

## Important Ideas & Architectural Components
* All the work on the machine is ultimately done by the kernel
* "Kernel land" is the land of core os, drivers and hardware
* "User land" is where user processes live
* User "root" lives in kernel land - so has no restrictions
* To cross from "user land" or "kernel land", user program make system library calls
* GRUB2 is the current, modern boot loader
* udev is the device manager
* dbus - interprocess communications mechanism
* sysfs - virtual file system mounted by the kernel that presents info about various kernel subsystems.
See /sys on the file system.
* procfs - presents info about processes. See /proc.
* Run levels
	* tell the system the "mode" in which to boot, e.g., 0=shut down, 3=normal boot
	* work via scripts ala systemd (older systems use init.d and /etc/inittab)
	* see /etc/systemd/system, /usr/lib/systemd/system
* Targets - serve a similar purpose of run levels
	* seems to be a more modern approach
	* targets are named (vs. numbered)
	* made up of _units_, which are declarative
* Partitions
	* divide storage into separate pieces
	* allows dual booting
	* separation of files
	* data organization
	* system protection
	* mounted to file system
* A shell is an interface into the OS
* In the shell
	* ; separates commands
	* \c escapes character c
	* single quoting hides special characters from the shell, e.g., echo 'ls; date' will prevent the shell from interpreting the ;
	* double quotes hide some metacharacters from the shell, but some are still processed, e.g., the $ is processed when
	used in double quotes
	
* Linux is very file-oriented - "everything is a file"
* Files are associated with one and only one *inode* (file metadata/admin data)
* Hard links point directly to inodes
* Symbolic links point to hard links, not directly to inodes
* To prevent the shell from interpreting wildcards before a command can interpret them, use '*'
* User ownership > group ownwerhip and Linux uses short-circuit evaluation on permissions
* Write permission to a **directory** enables deletion of files - even if you don't own the file!
* Sticky bit enforces that the owner of the directory or file is only allowed to delete a file
* VFAT is the only filesystem compatible among Windows, Linux and MacOS
* MTA = mail transfer agent, e.g., sendmail
