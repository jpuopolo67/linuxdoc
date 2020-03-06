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
* su - switch user (su - = open login shell)
  eg. su - to switch to root on centos (redhat)
* sudo -i (ubuntu)
* sudo <cmd> - run <cmd> as root
* wc - word/line count
* grep - filtering utility
* mandb - refresh man pages
* pinfo - a documentation system like man
* pwd - print working directory
* cd - change directory
* tr - translate characters
  
## Key Directories
/usr/share/doc - doc for installed packages

## Interesting Commands
uname -a | cut -d' ' -f1,2,3,4,5,6,7,8,9,10,11,12 | tr ' ' '\n'
uname -a | tr ' ' '\n'
