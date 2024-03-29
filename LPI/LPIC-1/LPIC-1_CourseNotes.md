# LPIC1 Course Notes

## DAY 01

VirtualBox

Alma Linux/Debian
Rocky/Debian

No GUI - 98% of certification focused on CLI
How to install GUI via CLI 

Recommended distro: for LPIC1 any distro is OK

Fedora
Ubuntu - is less recommended for LPIC1 certification, focused on ease of use - introducing distro specific tools (snap, plan)
RedHat
Debian
CentOS
Linux Mint
Rocky Linux
Alma Linux
Open SuSe

Ubuntu ll alias - ll is aliased to `ls -alF'

```Bash
# To view alias target
type <ALIAS>
type ll
# ll is aliased to `ls -alF

# -a, --all - do not ignore entries starting with .
ls -a

# sh prompt - $
# bash prompt - username@HOSTNAME:~$

```

### Exam Content

101: System Architecture
102: Linux Installation and Package Management
103: GNU and Unix Commands
104: Devices, Linux Filesystems, Filesystem Hierarchy Standard

### Essential commands

```Bash
# Current user
whoami
# Current host
hostname
# Path to working directory
pwd
# Help
## Usage manual
man
## Read info documents - information
info
## help command - when no man, whereis do not display location for such commands
help <command>
help fg
### those command are "shell bulletin"
type fg
### others are "hashed"
type mkdir
## --help switch for command

# Check whether it is file or directory and identify file type
file filename

# man section
# It is possible to create man files for your own commands/scripts or edit existing man files
# /usr/share/man - default main man directory, with sub-directories for man sections
# 1 : User command (executable programs or shell commands)
# 2 : System calls (functions provided by the kernel)
# 3 : Library calls (functions within program libraries)
# 4 : Special files (usually found in /dev)
# 5 : File formats and conventions eg /etc/passwd
# 6 : Games
# 7 : Miscellaneous (including macro packages and conventions),
# 8 : System administration commands (usually only for root)
# 9 : Kernel routines [Non standard]
```

In Linux everythnig is file.

Use of vi is an exam topic (103.8 Basic file reading).

- grep
- egrep
- fgrep
- sed
- regex

Certification is focused on bash interpreter.

### Bash KB shortcuts

### history

Stored in .bash_history hidden file (ls -A). Stored in memory when session closes correctly/gracefully (with exit) it gets written into .bash_history file - 1 file per user, from multiple sessions (reload on session start).

```Bash
# Clear up history - session buffer clear up
# for full clearup clear both buffer and file
history -c
# Specific line removal
history -d N
# Removing history file
rm -r .bash_history
# cat concatenates
cat .bash_history
# fmt allows formatting
fmt .bash_history
```

```Bash
# which only searches for executables / where does this command comes from? - Returns full path of (shell) commands
which ls
# whereis searches for any files - locates binary, source, and man page files for a command
whereis ls
```

**sudo = Switch User and Do**

```Bash
# sudo elevation - switch user and do
sudo COMMAND
# switch to sudo user
sudo su
# System info
uname -a

# echo
# double quotes - vars expanded
echo "This is my $HOME"
# single quotes - vasrs not expanded, literal output
echo 'This is my $HOME'

# alias
alias ALIAS=COMMAND
# to make it persistent add alias to bash.rc
```

## DAY 02

rm .bash_history

### Absolute/relative paths

Absolute path - starts from root /, in Win from drive letter.

In Linux we have 1 root, in Windows every drive has its own separate root starting from drive level (no common root).

### Data flows

Data flows/channels.

stdin[0] - input stream
stdout[1] - output stream
stderr[2] - error stream

```Bash
echo "Hola mundo"
# Write to txt file, overwriting existing file
echo "Hola mundo" > out.txt
# Write to txt file, appending to existing file
echo "Hola mundo" >> out.txt
# Below will output error to stderr[2] and nothing to file/stdout[1]
echno "Hola mundo" > out.txt
# Sending to 2 streams
find / -name interfaces 1> match.txt 2> error.txt
```

```Bash
/usr/bin/df -hT | grep -v loop
```

**/dev/null** - "black hole" - discards everything you send into it

Pipe - pass stdout of one command to stdin of another one.

ifconfig - deprecated package, alternative ip.

tr command - translate/delete characters, can be useful to replace space with some other symbol (" " > ";") to see more easily double spaces.

```Bash
# Replace char/letter
echo "Hola" | tr "H" "Z"
```

cut command - cut part of the file based on specified delimiter and column N ()

grep - print out lines which match patterns
```Bash
# Look up for user
cat /etc/passwd | grep mikhail
# Count cosequtive unique lines
uniq -c
# Order to make data consequtive
sort
```

/var/log/secure

### Aliases

alias - shows configured aliases


~/.bashrc, inside of it:

if [ -f ~/.bash_aliases ]; then
    . ~/.bash_aliases
fi

~/.bash_aliases

### Check/ban IP

https://www.ripe.net/ - entity which manages public IPs in EU, Russia

ripe.dm

whois

fail2ban
https://www.arsys.es/blog/instalar-fail2ban

/var/log/auth.log

clear / ctrl + L - clears screen by scrolling up
reset - deletes

### 103.2 Process text streams using filters

less is interactive command, you will need to exit yourself

less
/word_to_search

more is noninteractive command it exists itself

more

head
tail

tail -f

tac - cat backwards :)


```Bash
bzcat
cat
cut
head
less
md5sum
nl
od
paste
sed
sha256sum
sha512sum
sort
split
tail
tr
# uniq counts only consequitive lines as occurences, non consequtives will be counted separately
# can be used in combination with sort to workaround non-consequitive occurrences problem
uniq
wc
xzcat
zcat

# Number file lines, enter/line return counts for new line for the system
nl
cat -n file.txt
# in vi set list command will show line return as $ / set nolist to disable this
# cat -e to show end of line as $
cat -e file.txt

# sort by column, -n to specify numeric sort
sort -k 2 -t":" -n data.txt
# -R for random sort
alias voluntarion='sort -R students | head -l'
```

### Packaging/compression

Packaging - tar - no compression, just package into one file
Compression - gzip, bzip2, xz

To group files into package you package them, then compress

tar czf package.tar file*

File globbing VS regular expressions

Parameters: - Unix style, -- GNU style

## DAY 03

```Bash
ls /tmp/
mv /dir1/file1 /dir2/file2
# -f to suppress confirmation prompt
mv -f /dir1/file1 /dir2/file2
# "mv -i" = interactive = ask for confirmation, on RedHat distros mv is an alias to "mv -i"
# to create multple sub dirs _101, _102, etc.
#  -p, --parents - no error if existing, make parent directories as needed
mkdir -p lpi/exam_{101,102,201,202}/topics
# Remove the DIRECTORY(ies), if they are empty.
rmdir
# Remove directory with files
rm -rf /dir
# ls
#  -A, --almost-all - do not list implied . and ..
# -h, --human-readable - with -l and -s, print sizes like 1K 234M 2G etc.

# File Globbing, 3 types of globs (aka wildcards)
# * - any combination of any number of characters
# ? - any single character
# [] - matches the combination by exactly one character [A2] will return anything that contains A or 2
# ! - exclamation mark excludes characters from the list within the square bracket [!BC]
# ranges [a-z] and [0-9]

# grep with regex
# ^ beginning of a line
# $ end of a line
# all commented lines
grep "^#"
# all except comments - use -v = invert match
# remove comments (grep -v "^#") and empty lines (grep -v "^$")
cat .bashrc | grep -v "^#" | grep -v "^$"
grep -v "^#" .bashrc | grep -v "^$"

# File globbing VS regular expressions

# Search any number of spaces with end of line (empty line with N spaces) * = 0 to N occurrences
grep "^ *$" test.txt
# Eleminate such lines
grep -v "^ *$" test.txt

grep [3-5] /etc/passwd

# . any character in specific position only "1.3" will match 123, 113, 153 etc.
# .* - asterisk refers back to preceding char = any char any number of times from 0 to N

# Extended regular expressions
# grep -E =  -E, --extended-regexp PATTERNS are extended regular expressions
# +, ? - 1 or N times occurrence of preceding char or pattern, {} - number of repetition of preceeding char or pattern
# {1,3} = {min,max}

# () - groups of patterns
# Search for IPv4
# Look for 1 or 3 digits followed by literal dot and repeat 3 times
grep -E "([0-9]{1,3}\.){3}" test.txt
# 
grep -E "([0-9]{1,3}\.){3}[0-9]{1,3}" test.txt

# | - use more than one pattern (one or another)
grep -vE "^$|^#" test.txt

# non system users will have UID above 1000
# Users with home dir
 grep home.* /etc/passwd
```

#### 103.8 Basic file editing

```Bash
# Opening multiple "windows" inside of the same terminal
tmux
screen
# Ctrl + B, c - create, n - navigate, d - detach
tmux new -s "TMP"
tmux list-sessions
tmux a "TMP"
```

##### vi

3 modes:
- NAVIGATE
- INSERT
- EXECUTE

###### NAVIGATION

```
Esc Esc Esc : q !

Ctrl + C - will leave file.swp - with unsaved changes

H J K L = arrows, up and down go by line (EOL based, not visual)

gg - go to the first line
G - go to the last line
[N]G - go to line N
:N go to line N
/pattern + Enter - search for word descending, n to go the next occurence, N to go to
/?pattern - search for word ascending, n to go the next occurence, N to go to

0 - go to the beginning of a line
$ - go to the end of the line
w - jump by word/next word

u - undo
. - repeat

Go to Nth word:
[N]w next word
[N]b previos word

US KB ñ = :

dd - delete line (cut)
dw - delete word (cut)

Ndd - delete N lines (cut)
Ndw - delete N words (cut)
```

p - paste after
p - paste before

y - yank
[N]yy - copy N lines
[N]yw - copy N words

###### INSERT

To navigate - exit INSERT mode

To enter into insert mode:
i - insert text in cursor position
a - insert text after cursor
o - insert new line after current

I - insert text in the beginning of current line
A - insert text in the end of the line
O - insert new line before current

###### EXECUTION

:w - Write/Save
:q - Quit/Exit
:w [PATH] - Save as
ZZ  - Save & quit
:! command - open shell and run command
:r! command - open shell, run command and return output into document
:s/pattern1/pattern2 - replace first occurrence in current line
:s/pattern1/pattern2/g - replace all occurences in current line
:1,$s/pattern1/pattern2/g - replace all occurences in all lines

## DAY04

screen & tmux

grep

```Bash
echo "Este o este estereo estereotipo" | grep -E '((Est*)|(est*))'
# sin -E
echo "Este o este estereo estereotipo" | grep 'Este\|este'
# -i = case insensitive
echo "Este o este estereo estereotipo" | grep -i 'este'
# -w = search for word
echo "Este o este estereo estereotipo" | grep -iw 'este'
# -o = print  only  the  matched  (non-empty) parts of a matching line, with each such part on a separate output line
echo "Este o este estereo estereotipo" | grep -io 'este'
# count pattern match
echo "Este o este estereo estereotipo" | grep -iwo 'este' | wc -l
# -c = count lines with matching pattern (only lines, no matter how much it repeats per line)
echo "Este o este estereo estereotipo" | grep -iwc 'este'
# -q = quiet
# state variable, exit 0 (match found), exit 1 (match not found), exit 2 - error
grep -q 'este' info.txt

# -B n = show N lines preceding to match
grep -B 1 -iw 'banc[ao]' 

# recursive search through files for match
grep -r 'nameserver' /etc/
# also show line number
grep -nr 'nameserver' /etc/

# egrep, fgrep, rgrep = obsolete commands
# egrep = grep -E, fgrep = grep -F, rgrep = grep -r

# vi
# show line number - :set number
# hide line number - :set nonumber

# sed - replacements
# by default sed replace only 1st match on the line

sed s/[Ee]ste/norte info.txt

# Replace e with E on every line which has "b"
sed '/b/' 's/e/E/' colors.txt
```

```template.conf
<VirtualHost *:80>
    ServerName template.com
    ServerAlias webmaster@template.com

    DocumentRoot /var/www/html/template

    AccessLog /var/log/apache2/template-access.log
    ErrorLog /var/log/apache2/template-error.log
</VirtualHost>
```

```Bash
# Links - 2 types: soft & hard
# soft/weak link - direct access (via small independent shortcut file which takes small amount of disk space)
# hard link - do not use disk space
df -hT
# create 2 GB file
dd if=/dev/zero of=file1 bs=1M count=2000
ln file1 file2
ln -s file1 file_soft
ls -lh
rm file1
ls -lh
# inode - Linux FS works with inodes - structures which contain files' metadata which include pointers list
# Linux must allocate an index node (inode) for every file and directory in the filesystem. Inodes do not store actual data. Instead, they store the metadata where you can find the storage blocks of each file’s data.
# Check the inode number in a specific file
ls -i
# Check the inode usage on FSs
df -i

# Search by name
find / -name "TestFile"
# Search by type
# f = file
find / -type f
# i = inum
find / -type f -inum 130775 2> /dev/null

# Processes in Linux
# LPIC1 focuse exclusively on top
top
# top load average should be below 1
# top KB shortcuts
# k - kill process

# swap
# free -h to seee available memory & swap info
# allows to see if swap is being used while RAM is unused
free -h
# buffers data waiting to be placed to disk - CPU maybe working on them still
# cache data stored to disk - already processed data
free -h -w

# bashtop
bashtop

# ps - report a snapshot of the current processes, within current session
# ps -ax - report a snapshot of the current processes, within all sessions

# who - Print information about users who are currently logged in.

# zombie process - process which is not terminated and do not have parent process, state code Z
# S - sleep
ps -ax
ps -ax -o pid,stat | grep Z

ps -ax | grep ping

ps -ax -o pid,ppid,tty,cmd | grep PID

# zombie clear up
kill -HUP $(ps -A -ostat,ppid | grep -e '[zZ]'| awk '{ print $2 }')

# kill -2 = send signal 2 ~ Ctrl +C, do not work for processes running in foreground
# kill -19 = pause process
# kill -18 = resume process

# jobs -  Lists the active jobs.  JOBSPEC restricts output to that job.
# Without options, the status of all active jobs is displayed.
jobs --help

# fg PID - bring process to foreground

# Kill key statuses
# 2 - SIGINT - the signal sent when we press Ctrl+C. The default action is to terminate the process. However, some programs override this action and handle it differently; "interruption request sent by the user"
# 9 - SIGKILL - "kill"; When a process receives SIGKILL it is terminated. This is a special signal as it can’t be ignored and we can’t change its behavior.
# We use this signal to forcefully terminate the process. We should be careful as the process won’t be able to execute any clean-up routine.
# 15 - SIGTERM - "exit"; terminate the process but specifically requesting to finish it, SIGTERM is the default signal when we use the kill command. When we send SIGTERM, the process sometimes executes a clean-up routine before exiting and it also can be handled to ask for confirmation
# 18 - SIGCONT - "continue" 
# 19 - SIGSTOP - "pause"
```

```Bash
# Loop example
for i in apple manazana orange ; do echo $i ; done
```

## DAY05

File permissions

chmod

9 bits, 3 groups [---][---][---]

- owner rwx
- group owner rwx
- others rwx

```Bash
# To see user ID and user's groups IDs
id username
# Remove execute rights
sudo chmod -x /usr/bin/firefox
# View permissions
# Current dir
ls -ld
# Specific file within current dir
ls -ld file1.txt
# X permission required to traverse directory content ~ access to a directory (user will be able to view directory contentent but not to enter into it
# In Linux directory is a file which contains 2 columns - resource/file name and corresponding i-node number
# Root directory is always i-node 2, all others have random number
# To view file in directory we look into folder i-node and then move on to file i-node
# Directory R = check directory content
# Directory X = access directory conten
```

Permission management - symbolic notation or base-8 notation (0-7)

| base-8 | binary | RWX |
|--------|--------|-----|
| 0      | 000    | --- |
| 1      | 001    | --x |
| 2      | 010    | -w- |
| 3      | 011    | -wx |
| 4      | 100    | r-- |
| 5      | 101    | r-x |
| 6      | 110    | rw- |
| 7      | 111    | rwx |

```Bash
# Change file owner
chown user file
```

Symbolic notation

Useful when you need to add/remove permissions for entity

echo 'echo "Hello world!"' > script.sh
chmod +x script.sh
./script.sh

Entities
u - User
g - Group
o - Owner

Operations
+ - add
- - remove
= - set

Permissions
r - Red
w - Write
x - Execute

./ - reference to current directory

```Bash
# Look for files with 777 permissions
find /etc/ -type -f perm 777
# touch - updates 3 time stamps of existing file (access, modify, change) but not birt time stamp
touch file1.txt
stat file1.txt
```

Change group ownner

```Bash
# Change the group of each FILE to GROUP.
chgrp
# With chown
chown :group file
```

Practice:

```Bash
# PART1
# Obtener la MAC del interface ens3 usando el comando ip address show
ip a show eth0 | grep -Eoh '[a-fA-F0-9]{2}(:[a-fA-F0-9]{2}){5}' | grep -v 'ff:ff:ff:ff:ff:ff'
ip a show eth0 | grep ether | cut -d" " -f6
ip a show eth0 | awk '/[a-fA-F0-9]{2}(:[a-fA-F0-9]{2}){5}/'
ip a show | grep ether | awk '{print $2;}'
# Mostrar la hora actual, solamente la hora
# Only current hour
date "+%H"
# Current time HH:MM:SS
date "+%T"
# cut issue - column number will vary depending on region/format settings of your system
date | cut -d' ' -f 5
# Cambiar las minúsculas a mayúsculas de la palabra Hola
echo "HolA" | tr a-z A-Z
echo "HolA" | tr [:lower:] [:upper:]
# Mostrar el contenido de /etc/passwd sustituyendo los dos puntos “:” por espacios “ ”
cat /etc/passwd | tr ":" "  "
sed 's/:/ /g' /etc/passwd
# Líneas que contiene la cadena de caracteres admin en el fichero /etc/passwd
cat /etc/passwd | grep admin
# Muestra los campos 1, 3 y 7 del fichero /etc/passwd
cat /etc/passwd | cut -d":" -f1,3,7
# Muestra a partir del tercer campo del fichero /etc/passwd
cat /etc/passwd | cut -d":" -f3-
# Muestra el nombre de usuario, el UID y el shell del usuario pue
cat /etc/passwd | grep mikhail | cut -d":" -f1,3,7
# Número de líneas y de palabras del fichero /etc/passwd
cat /etc/passwd | wc -l
cat /etc/passwd | wc -w
wc -lw /etc/passwd
#Número de usuarios del sistema que utilizan /bin/bash como shell
grep /bin/bash /etc/passwd | wc -l
# More exact so that we look for the match before the end of the line
grep /bin/bash$ /etc/passwd | wc -l
# Muestra el fichero /etc/passwd en orden alfabético 
sort /etc/passwd
# Muestra el fichero /etc/passwd ordenado por UID en de forma inversa
sort -k3 -t":" -n -r /etc/passwd
# Pasar las vocales a mayúsculas de la palabra murcielago
echo "murcielago" | tr [aeiou] [AEIOU]
# Mostrar el contenido de la carpeta actual en formato largo, ordenado de forma ascendente por tamaño

# Mostrar por pantalla las líneas que contienen comentarios en el archivo /boot/grub/grub.cfg
# Enviar a un fichero las líneas del archivo /boot/grub/grub.cfg que no son comentarios
# Mostrar las líneas de un fichero que contienen la palabra BADAJOZ o HUELVA, numerando las líneas de salida
# Mostrar los ficheros que contienen la palabra "interface" en el directorio /etc/ y sus subdirectorios
# Buscar los 5 municipios con mayor superficie
# Buscar cuantos municipios hay en la provincia de Tarragona

# PART2
Muestra un salto de línea
Muestra una tabulación
Muestra las líneas del fichero /etc/network/interfaces numerándolas
Muestra las líneas del fichero /etc/network/interfaces numerándo sólo las líneas con contenido
Muestra las primeras 7 líneas del fichero /etc/passwd
Muestra las últimas 7 líneas del fichero /etc/passwd
Muestra las primeras 3 líneas de todos los ficheros .log del directorio /var/log
Busca dentro de los ficheros del directorio /var/log el patrón root
Ordenar, en orden inverso, las líneas del fichero /etc/passwd
Ordena el fichero /etc/passwd utilizando el campo UID como criterio de ordenación
Calcula el número total de titulos que hay en todos los ficheros del directorio /usr/share/data/peliculas/, descartando títulos repetidos
Indica el número de veces que aparece la palabra "molino" en el fichero "el_quijote.txt"
Dividir el fichero ripe.db en ficheros de 10M
Buscar la ubicación del comando fdisk dentro de todo el sistema
Identificar la versión del kernel que estamos usando
```

echo $$ - returns PID of bash

## DAY06 19.09.2022

### Topic 102: Linux Installation and Package Management

#### 102.1 Design hard disk layout

### Topic 104: Devices, Linux Filesystems, Filesystem Hierarchy Standard

#### 104.1 Create partitions and filesystems

GRUB - Linux boot manager
NTLOADER - Windows boot manager

Hardware boot up
- BIOS POST

HDD physical structure
- Spindle
- Track t
- Sector s
- Cylinder c
- Platter
- Arm

SSD also have physical sectors - blocks, 512 bytes

Parked read-write head are alwats in 0/0/0 (track/sector/cylinder)

1st sector of disk is called MBR and it stores boot loader.

UEFI

[About Solid State Drives (SSD)](https://www.oo-software.com/en/docs/whitepaper/whitepaper_ssd.pdf)

SSD layout

In contrast to the hard disk, a SSD consists of semiconductor memory building blocks, it contains no mechanical parts. The smallest unit of an SSD is a page, which is composed of several memory cells, and is usually 4 KB in size. Several pages on the SSD are summarized to a block. A block is the smallest unit of access on a SSD. Currently, 128 pages are mostly combined into one block; therefore, a block contains 512 KB.

Hard disk alignment

CHS (cylinder head sector) alignment

The alignment on cylinder head sector indicates an addressing method that introduces the geometry of the hard disk with the hard disk controller. This allows it to read data from a disk or write to one.

SSD alignment

Unlike hard disks, SSDs use a different algorithm to determine the first logical sector. The data are always read and written in blocks. Therefore, partitions / volumes need to always be aligned in blocks on SSDs. From Microsoft Windows Vista on a non - CHS orientation is supported by Windows. In the registry under
„HKEY_LOCAL_MACHINE\SYSTEM\CURRENTCONTROLSET\SERVICES\VDS\ALIGNMENT“ are default values, which can be modified by the administrator. From a disk size of 4 GB on, the values stored are 1 MB. This value, 1 MB, is a multiple of the standard block size of 512 KB for SSDs and a multiple of 64KB at a CHS alignment. In this way, Windows ensures that both disks can work optimally.

sudo fdisk -l

4 primary partitions
1 primary partition can be converted to extended, so that 3 logic partitions can be created within it

###  Loop device

In Unix-like operating systems, a loop device, vnd (vnode disk), or lofi (loop file interface) is a pseudo-device that makes a computer file accessible as a block device. Before use, a loop device must be connected to an extent file in the file system. The association provides the user with an application programming interface (API) that allows the file to be used in place of a block special file (cf. device file system). Thus, if the file contains an entire file system, the file may then be mounted as if it were a disk device.

Files of this kind are often used for CD ISO images and floppy disk images. Mounting a file containing a file system via such a loop mount makes the files within that file system accessible. They appear in the mount point directory.

```Bash
# Partitioning
fdisk
gdisk
parted
# UI/frontend which calls other commands (fdisk & mkfs)
gparted
# mke2fs
mkfs
```

### System installation and folders

On Ubuntu clean install su - does not work/as root user is inactive.

```Bash
# df - Show information about the file system on which each FILE resides, or all file systems by default.
# -h, --human-readable  print sizes in powers of 1024 (e.g., 1023M)
# -H, --si              print sizes in powers of 1000 (e.g., 1.1G)
df -h
# Info on installed distro/OS
cat /etc/os-release
```

#### The file system essential standard (FHS)

Essential Programs
Non-essential Programs

```Bash
# User's scripts - /usr/local/bin
/usr/local/bin
# Software from vendors - /opt
/opt
# Config files - /etc
/etc
# Users' homes (/home/username)
/home
# drwxr-xr-x root root
# root user home directory /root
ls -ld /home
#
/mnt
# Removable media devices mount point
/media
# Insert flash drive and check
sudo fdisk -l | grep sd
# 
/boot
# mount point for detected devices
/dev
/dev/pts
echo "Hola" > /dev/pts/1
# Zeroes partition
/dev/zero
/dev/null
/dev/random
```

Next class:

Kernel & modulos

Aliases for partitions
linux    - 83
swap     - 82
extended - 05

## DAY07 21.09.2022

```Bash
# -h - human readable format, -w - wide output
free -h -w
# Change hostname
vi /etc/hostname
hostname -F /etc/hostname
#
vi /etc/fstab
# df - Show information about the file system on which each FILE resides, or all file systems by default.
df
df -hT -t ext4 -t ext3
# 
blkid
# man section 5 , in Ubuntu 22.04 section 8
# 5   File formats and conventions, e.g. /etc/passwd
# 8   System administration commands (usually only for root)
man fstab
```
### Pseudo File Systems

The objects within pseudo file system structure simply represent real resources and their attributes, pseudo filesystems are generated dynamically when your computer boots.

suid/nosuid

FS Dependent Mount OPtion

| Options               | Description                                       |
|-----------------------|---------------------------------------------------|
| acl/no acl            |                                                   |
| commit=               | frequency of synchronization of journal meta data |
| data=                 |                                                   |
| errors                |                                                   |
| userquota/nouserquota |                                                   |
| nonrecovery/noload    |                                                   |


```Bash
#
nmap
```

### LVM (LogicaL Volume Management)

```Bash
find . -type f -name "*lvm*"
```

LVM is an additional logical layer on top of partitions.

LVM uses the acronym PV to represent a physical volume, VG for volume groups (collections of one or more physical volumes), and LV for logical volumes.

- Disks > Physical volumes / Partitions
- Logical Volumes > Volume Groups (can combine various disks)
- Mount points

```Bash
pvcreate
# To create a new volume group, you use the vgcreate command and specify the name you’d like to give your group and the physical partitions you want to include:
sudo vgcreate my-new-vg /dev/sdb2 /dev/sdb3
```

### Distributions

Debian and RedHat - two big parents/branches from which other distros are forked.

cat /etc/os-release

Ubuntu releases every 6 month 22.04 > 22.10 > 23.04 (+6M step)
Every 2 years LTS version, i.e. version which has 3 years support, others 18 months.
Ubuntu code names - Adjective + Animal starting from the same letter

Debian - codenames Toy Story chars

```Bash
# locate VS find
locate
# find has lots of options - where & what to search + fitltros
find /mnt -type f -name "abc*.pdf"
find / -type f -name "abc*.pdf"
find / -type f -name "abc*.pdf" -size +1M 
find /etc/ -maxdepth -type f -name "*.conf"
find / -maxdepth 2 -type f -name "*.conf"
```

## 08 28.09.2022

reload VS restart: reload - re-read config file, restart - restart service (interruption, dropping active connections)

```Bash
sudo system set-default reboot.target
# units
# vendor - e.g. vsftpd.service etc.
# /usr/lib/systemd/system/
# custom
# /etc/systemd/system -
#
# /run/systemd/system - units created at execution time
# 
systemctl isolate multi-user.target
```

[Cómo usar Systemctl para gestionar servicios y unidades de Systemd](https://www.digitalocean.com/community/tutorials/how-to-use-systemctl-to-manage-systemd-services-and-units-es)


Installation of Linux apps

sudo apt-get install ifconfig
sudo apt-cache search ifconfig

Repositories - public software servers

Dependencies tree

sudo apt-get install + TAB - will return total count of packets in all repositories - Display all 68655 possibilities? (y or n)

In majority of cases package is called/named exactly the same as a command.

sudo vi /etc/apt/sources.list

After updating package list run sudo apt-get update

RedHad derived systems do not have local repo cache.

apt-get install apache

Debian
- apt-get update - updates list of available packages
- apt-get upgrade - update installed packages

RedHat (yum)
- yum update - update packages + preserve obsolete packages
- yum upgrade - update packages + delete obsolete packages

## 09 03.10.2022

### GRUB

#### GRUB Legacy vs. GRUB 2

The original version of GRUB (Grand Unified Bootloader), now known as GRUB Legacy was developed in 1995 as part of the GNU Hurd project, and later was adopted as the default boot loader of many Linux distributions, replacing earlier alternatives such as LILO.

```Bash
#grub>
# list/identify devices
ls
#
```

```Bash
# List libraries used by program
ldd
# LD_LIBRARY - variable to add routes to search for libreries
# ld.so.config - config file to add additional routes to search for libraries (global)
```

### 102.4 Use Debian package management

```Bash
# directory you can add files with additional repositories to be used by APT, without the need to modify the main /etc/apt/sources.list file
/etc/apt/sources.list
# install a .deb package
dpkg -i <package_name>
# dpkg-reconfigure
# apt-get
# apt-cache
```

Debian Package Managers

- **dpkg** - Debian package format (.deb) and its package tool (dpkg), they are widely used not only on Debian itself, but also on its derivatives, like Ubuntu and those derived from it.
- **Advanced Package Tool (apt)** - another package management tool that is popular on Debian-based systems, can streamline many of the aspects of the installation, maintenance and removal of packages, making it much easier.

The Advanced Package Tool (APT) is a package management system, including a set of tools, that greatly simplifies package installation, upgrade, removal and management. APT provides features like advanced search capabilities and automatic dependency resolution. APT is not a “substitute” for dpkg. You may think of it as **a “front end”, streamlining operations and filling gaps in dpkg functionality, like dependency resolution**.

### 102.5 Use RPM and YUM package management

- **RPM Package Manager (rpm)** - is the essential tool for managing software packages on Red Hat based (or derived) systems.
- **YellowDog Updater Modified (YUM)** - yum was originally developed as the Yellow Dog Updater (YUP), a tool for package management on the Yellow Dog Linux distribution. Over time, it evolved to manage packages on other RPM based systems, such as Fedora, CentOS, Red Hat Enterprise Linux and Oracle Linux.


## 10 05.10.2022

### Well known ports (below 1024)

20 - FTP / TCP
21 - FTP 
22 - SSH/SFTP
23
25
53 - DNS / TCP - between servers/UDP - from client to server
80 - HTTP / TCP
110 - POP3
443 - HTTPS

```Bash
nmap localhost
ss -tlp4
grep 3389 /etc/services
```

#### TCP VS UDP (Layer 4)

| TCP                                           | UDP                                                                        |
|-----------------------------------------------|----------------------------------------------------------------------------|
| - Connection oriented                         | - Not connection oriented                                                  |
| - Confirmation of transfer                    | - No confirmation                                                          |
| - Re-try/re-transfer                          |                                                                            |
| - Priority: data integrity (email, web pages) | Priority: latency/speed, loosing some packets acceptable (streaming, VoIP) |

OSI/TCP-IP - layered models which split tasks/work between different layers

#### ICMP (Layer 4)

ICMP = Internet Control Message Protocol, ping

ping - check if connectivity works/exists, response time, packet lose rate and whether target machine/device is up

```
for i in 'cat ports'
```

#### IPv4

Notation: 4 octets of 8 bits = 32 bits address

Address space: 2^32 = 4,294,967,296

Classes:
A 0-127 / 0 MASK 8
B 128-191 / 10 MASK 16, max hosts = 65,534
C 192-223 / 110 MASK 24, max hosts = 
D 224-239 / 111

8 bit mask, 24 bit host, max N of hosts 2^24 = 16,000,000

Private IPs are non routable (stay within LAN), public IPs are routable.

**APIPA**

In computer networking, a link-local address is a network address that is valid only for communications within the subnetwork that the host is connected to. Link-local addresses are most often assigned automatically with a process known as **stateless address autoconfiguration** or **link-local address autoconfiguration**, also known as **automatic private IP addressing (APIPA)** or **auto-IP**.

Link-local addresses are not guaranteed to be unique beyond their network segment. Therefore, routers do not forward packets with link-local source or destination addresses.

IPv4 link-local addresses are assigned from address block **169.254.0.0/16 (169.254.0.0 through 169.254.255.255)**. In IPv6, they are assigned from the block **fe80::/10**.

```Bash
ipcalc 192.167.22.12/23
```

#### Subnetting

#### Networking commands

```Bash
# View interface information, configure IP, show link state
ip a
ip as
ip address show
ip route show
ip route add
ip route del
# Activate interface promiscuous mode
sudo ip link set eth0 promisc on
# Assign IP (not persisten, persistent via config file)
sudo ip address add 192.168.1.11 dev eth0
# Show network devices
ip link show
# Show ARP table
ip neigh show

ifconfig # deprecated
ifup
ifdown
netstat # deprectated
ping
nmap
route # deprecated
tracert
dhclient
telnet
ssh
```

## 11 10.10.2022

### Vagrant

### IPv6

Hexadecimal

0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16
0 1 2 3 4 5 6 7 8 9 A  B  C  D  E  F  

2 ^ 128

16 bit x 8 = 128 bit, : as a separator

32 hexadecimal symbols

Compression/abbreviation rules:
- Leading 0s can be omitted
- Sequence of 0s - ::, once per address

Network prefixes
- IPv4  - we use prefixes 255.255.255.0 or /24 etc.
- IPv6 - /64 half of address goes to subnet mask, we only use prefixes (/N)

2001.0000.0000.0000.0000.0000.0000.0001 = 2001::1

- No broadcast concept, only unicast
- 2000::/3
- Global unicast - similar to public IPv4 - unique & routed, all which start from 001 (binary) - 2000::/3 to 3FFF::/3
- Modified EUI-64 Format - creates host part based on 48-bit MAC address


Subnetting

- /16 /32 /48 /64 /80 /96 /112
- Local-link

Exam IPv6 questions:
- IPv6 notation
- Contraction/abbreviation rules
- Masking (only prefix masks)
- Global unicast prefix - 
- Link local prefix - FE80 - FEFF

Network Configuration Files

```Bash
/etc/hostname # machine name
# edit file and restart machine or
sudo hostname -F /etc/hostname
/etc/hosts # hos resolution entries
/etc/nsswitch.conf # DNS reolving order - hosts: files dns, if we change order hosts file won't have priority
/etc/resolv.conf # DNS servers
/etc/network/
/etc/network/interfaces # NIC/interfaces definitions
```

```Bash
tcpdump # CLI sniffer, network tracer utility
tcpdump -n -i enp0s8 icmp
it route show
iptables # configure NAT
nmcli # netork manager, allows to create connections and apply configurations
nmcli connection up <connection_name>
```

## 17.10.2022

```Bash
# ip - show / manipulate routing, network devices, interfaces and tunnels
ip link # verify whether interface is up
ifup eth0 # enable interface, ifdown to disable
ip a # address
ip r # route
# ifconfig - configure a network interface / deprecated command
ifconfig
ifconfig enp0s3 192.168.178.32 netmask 255.255.255.0 # add IP configuration
vi /etc/network/interfaces # add PERMANENT IP configuration
# iface eth1 inet static
#   address 10.0.0.1
#   netmask 255.255.255.0
#   gateway 192.168.109.1

# after making changes to IP configuration , ifdown/ifup to apply

# default gateway = default route
route add default via 10.0.0.254 # temp, for permanent change edit configuration file /etc/network/interfaces

# open ports

ping
ping -I eth0 192.168.109.1 # ping through specific interface
route # print out route table
traceroute
systemctl ssh

# nmap - scan ports
nmap -sn 10.0.0.0/24 -oA results.txt

# when correct IP is unknown we can try to discover it by putting interface in promiscuos mode and using tcpdump
ip link set eth1 promisc on
tcpdump -n -i eth1

ip address show # will show all interfacess as all of them have MAC address
ip -4 address show # will only show interfaces with IPv4 assigned

# change MAC address
ip link set eth1 address

# Deprecated commands - arp, route, ifconfig, netstat
# arp, route, ifconfig > superceded by ip
# nstat > superceded by ss
nmap # scan remote machines or local host for open ports
netstat # check local host for open ports - open connections/listening connections

# -u -include UDP, -t include TCP, -p include PID, -a - all (listening/established)
# -tl - solo TCP listening
# -n - do not translate port number into protocol/serv name (e.g. 443 into HTTPS) - based on /etc/services file contents
netstat -punta | head -5
```

Network Troubleshootinh Flow:
- Check if interface is up - iplink show, iplink eth1 up
- Check if IP config is correct - 
- Check if GW is reachable
- Try alternative/other interface
- Check for othet GW with nmap
- Create new route
- Document
- Close ticket

```Bash
# 2 ways to check opened connections to specific ports:

# lsof - list open files
lsof -i:22

# netstat
netstat -tl

# ping, -s 1500 set packet size
# -f - flood ping, for every ICMP send print . for reply erase - line grows = number of lost packets increases, ideally should be stable short line

# traceroute, generates trace to reach target

# mtr - a network diagnostic tool, my trace route
# sustained trace, keeps repeeting trace and generating stats
mtr -n domain.con
```

time-outs/microcortes
bottleneck

default max hop N = 30

Default TTL and Hop Limit Values

Default TTL and Hop Limit values vary between different operating systems, here are the defaults for a few:

- Linux kernel 2.4 (circa 2001): 255 for TCP, UDP and ICMP
- Linux kernel 4.10 (2015): 64 for TCP, UDP and ICMP
- Windows XP (2001): 128 for TCP, UDP and ICMP
- Windows 10 (2015): 128 for TCP, UDP and ICMP
- Windows Server 2008: 128 for TCP, UDP and ICMP
- Windows Server 2019 (2018): 128 for TCP, UDP and ICMP
- MacOS (2001): 64 for TCP, UDP and ICMP

speedtest-cli

/etc/network/if-up.d

ssh - tunnels & port forwarding

```Bash
# Get FQDN
host
dig
# DNS records - A, NS, MX, CNAME (alias), PTR (name to IP)
host -t A facebook.com
host -t PTR facebook.com
host -t NS cocacola.com
```

## 19.10.2022

```Bash
man sudo
whoami
# execute command as root
sudo -u root whoami
# switch to root
su -
# In Ubuntu root user
# Best practice work with personalized/identifiable users instead of shared/generic users
# If we omit -u username it is implied that we want to use -u root
cat /etc/passwd | cut -d":" -f1 | xargs id | grep sudo
# sudoers file
# This file MUST be edited with the 'visudo' command as root - it will check syntax check before saving
sudo cat /etc/sudoers
sudo visudo
# .ssh/ - id_rsa, id_rsa.pub
# ./ssh/authorized_keys
# run command over ssh
ssh user@host tail -3 /etc/passwd

# sudoreplay
sudoreplay

# /etc/sudoers.d/

Cmnd_Alias SOFTWARE = /usr/bin/apt-get install *, !/usr/bin/apt-get install nano, !/usr/bin/apt, !/usr/bin/dpkg

%teachers ALL=(ALL:ALL) NOEXEC: DISK, !FILES, EDITOR, NETWORK
%students

# ssh profiles
ssh 0 = ssh -i ~/.ssh/keys/my_key root@zero

# Password policies
/etc/ssh/sshd_config # system-wide configuration file for OpenSSH which allows you to set options that modify the operation of the daemon
# specify custom port
Port 22

# disable password auth for everyone
PasswordAuthentication no

# root ssh private key login only 
PermitRootLogin prohibit-password
# root ssh login completely disabled
PermitRootLogin no

DenyUsers user1 user2
AllowUsers user3 user4

# pam modules
/etc/pam.d

# scripts
./script.sg
source script.sh

# First line indicates shell agains which script will be executed
# #! /bin/bash

source ~/.bashrc
. ~/.bashrc
```

## 24.10.2022

```Bash
# Adding variables - local level applied after global, so for the same var user will have a value from local config
# Global config
cat /etc/profile
/etc/bash.bashrc
# Local config
~/.profile
~/.bashrc

# Users Management
# Permissions - Owner - Group - Others
# User will have a group with the same name as user when you provide no group name for user

sudo user add user1
sudo passwd user1
mkdir /home/user1
chown user1 /home/user1

# -d can be other location as /home - it is just working directory immediately after user login
# on Apache servers home can be something like /var/www/html/website1
# -u to specify UID, e.g. -u 543
sudo useradd user2 -g users -m -d /home/user2

# command will also create the following
# .bash_logout
# .bashrc
# .profile
# .ssh

sudo useradd mike -u 2021 -g 1002 -m -d /home/mike -s /bin/bash
# -k, --skel SKEL_DIR = use this alternative skeleton directory
sudo useradd john -u 2022 -g 1002 -m -d /home/mike -s /bin/bash -k /usr/share/skel
# you can use alternative skeleton directory to preload your public key on all machines

# /etc/passwd contains a list of the system's accounts, giving for each account some useful information like user ID, group ID, home directory, shell, etc.
/etc/passwd

bin:x:1:1:bin:/bin:/sbin/nologin # sbin/nologin displays a message that an account is not available and exits non-zero. It is intended as a replacement shell field to deny login access to an account.
# If the file /etc/nologin.txt exists, nologin displays its contents to the user instead of the default message.
# The exit code returned by nologin is always 1.

# usermod - to modify user
# Modify primary group -g
sudo usermod user1 -g admins
# Add additional group -G
sudo usermod user1 -G FTP

# Delete user
userdel

# Group management
groupadd
groupmod
groupdell

# Password management
passwd
chage
# List password expiration details for user
sudo chage -l user

### Create user script - interactive

#! /bin/bash

#echo -n "User name for new user?"
#read NAME

NAME=$1

grep -q $NAME /etc/passwd

if [ $? -eq 0 ]
then
    echo "User $NAME already exists"
else
    useradd $NAME -g users -m -d /home/$NAME
fi

### If example
# save as file +  chmod +x test.sh
# then run test.sh apple manzana banana
if [ $# -eq 3 ]
then
    echo $1
    echo $2
    echo $3
else
    echo -n "You didn't pass in 3 variables, but "
    echo $#
fi

echo $0

### Loop example
# for - finite loop
# Loop through command result - $(seq 1 20) - one line
for i in $(seq 1 20) ; do echo $i ; done

## while - condition based loop - one line
x=1; while  [ $x -le 5 ]; do echo "Welcome $x times" $(( x++ )); done
## while - condition based loop - multi line

#!/bin/bash
x=1
while [ $x -le 5 ]
do
  echo "Welcome $x times"
  x=$(( $x + 1 ))
done

### Options Selector - case

## languages.sh example

#!/bin/bash

echo -n "Enter the name of a country: "
read COUNTRY

echo -n "The official language of $COUNTRY is "

case $COUNTRY in

  Lithuania)
    echo -n "Lithuanian"
    ;;

  Romania | Moldova)
    echo -n "Romanian"
    ;;

  Italy | "San Marino" | Switzerland | "Vatican City")
    echo -n "Italian"
    ;;

  *)
    echo -n "unknown"
    ;;
esac

```


## 26.10.2022

### Logging

facility.priority

**facility** - This component represents the process, modules, or protocols that created the syslog event. It could be the mail system, the kernel, clock, line printer, network, etc.

**priority** - A single digit ranging from 0 to 7 that determines the importance of the reported event.

Priority levels
- 0	/ Emergency	/ emerg
- 1	/ Alert / alert
- 2	/ Critical / crit
- 3	/ Error / err
- 4 / Warning -	Something will happen if it is not dealt within a timeframe.
- 5 / Notification - Normal but significant conditions.
- 6 /Informational - Informative but not important.
- 7 /Debugging - Lots of unnecessary messages. Only relevant for developers

 Different types of facilities recognized by Linux:

- auth or authpriv: Messages coming from authorization and security related events
- kern: Any message coming from the Linux kernel
- mail: Messages generated by the mail subsystem
- cron: Cron daemon related messages
- daemon: Messages coming from daemons
- news: Messages coming from network news subsystem
- lpr: Printing related log messages
- user: Log messages coming from user programs
- local0 to local7: Reserved for local use

List of priorities in ascending order:

- debug: Debug information from programs
- info: Simple informational message - no intervention is required
- notice: Condition that may require attention
- warn: Warning
- err: Error
- crit: Critical condition
- alert: Condition that needs immediate intervention
- emerg: Emergency condition


```Bash
ls -l /var/log # logs directory
vi /etc/rsyslog.conf # Logging configuration - rsyslog.conf - rsyslog daemon config
# where to send - folder/remote machine
cat /etc/logrotate.d/rsyslog # logs rotation, N weekly = every N weeks
# Modules
# imudp/imtcp for remote logs sending
# Log by facility
sudo systemctl restart rsyslog.service
logger # allow to enter messages into the system log

# journalctl
# More filtering options, store logs in DB
# by default /ecc/
cat syslog | grep cupsd
journalctl -u UNIT
# -u [UNIT]
# -since=
# -until=
# -b [N] - system start messages where 0 is current start, 1 previous start
```
### Task Scheduling - crontab (user/system-wide)

```Bash
# Tasks scheduling - periodic programmatic tasks
crontab -e # edit cron tasks for current user, user field is not configurable
/etc/crontab # system-wide crontab
atq # view scheduled tasks queue

# Job definition has 5 fields to define run schedule
# and 2 more - who runs task (root) & task to be executed/path to script

# 00 10 4 7 1,5 - every 4th of July if it is work day work days
# 1-5 range
# */10 fraction, e.g. every 10th minutes of N hour etc.
# maximum frequency - * * * * * = every minute, can't be lower with cron

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name command to be executed
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
###

crontab -u mikhail
sudo ls /var/spool/cron/crontabs
/var/logs/cron
# For better security we need to deny cron editing to anyone except specific user(s) who need that
/etc/cron.allow
/etc/cron.deny

# The same fot tasks
/etc/at.allow
/etc/at.deny

# anacron - missed tasks will be re-run on reboot
/usr/sbin/anacron
```

### GUI

Major GUI environments

- GNOME
- KDE
- Unity
- MATE
- Cinnamon

```Bash
# If not empty, then GUI is present
echo $DISPLAY
# xorg - GUI server
whereis xorg
```

X window system DISPLAY consists (simplified) of:

- a keyboard
- a mouse
- a screen.

A display is managed by a server program, known as an X server. The server serves displaying capabilities to other programs that connect to it.

ttl/1
pts/1

**xorg** or **wayland** - **display server**, it requires **window manager** for additional features (multiple windows and closing/moving of those, etc.), e.g. **openbox**, and further session manager, e.g. **Openbox** (stacking window manager for the X Window System).

Graphical Environment
Major Desktop Environments (GNOME, KDE, Unity, MATE, Cinnamon, XFCE, LXDE)

#### Accessibility Options - 106.3

High Contrast
Zoom
Large Text
Screen Reader

## 107.3 Localisation and internationalisation

- Configure locale settings and environment variables.
- Configure timezone settings and environment variables.

/etc/timezone
/etc/localtime
/usr/share/zoneinfo/
LC_*
LC_ALL - set the same config for all settings
LANG
TZ
/usr/bin/locale
tzselect
timedatectl
date
iconv
UTF-8
ISO-8859
ASCII
Unicode

## 108.4 Manage printers and printing - CUPS

- Basic CUPS configuration (for local and remote printers).
- Manage user print queues.
- Troubleshoot general printing problems.
- Add and remove jobs from configured printer queues.

- CUPS configuration files, tools and utilities
- /etc/cups/
- lpd legacy interface (lpr, lprm, lpq)

```Bash
# http://127.0.0.1:631/
systemctl status cups
/etc/cups/cupsd.conf # config file

# Only listen for connections from the local machine.
Listen localhost:631
Listen /run/cups/cups.sock

/etc/cups/printers.conf

lp text.txt printer_name # print file
lpq # print queue
lprm # empty print queue / cancel all jobs
```

### 108.3 Mail Transfer Agent (MTA) basics

- Create e-mail aliases.
- Configure e-mail forwarding.
- Knowledge of commonly available MTA programs (postfix, sendmail, exim) (no configuration)

~/.forward
sendmail emulation layer commands
newaliases
mail - CLI MUA to send emails
mailq
postfix
sendmail
exim

MTA - Mail Transfer Agent = SMTP / local level, port 25
MDA - Mail Delivery Agent = POP/IMAP
MUA - Mail User Agent = Email Client App


```Bash
mail -s "Help" # Send email with subject Help, Ctrl+D to send

# mail aliases
vi /etc/mail/aliases
# postmaster: root
# helpdesk: mikhail

# The newaliases utility makes changes to the mail aliases file visible to smtpd(8).  It should be run every time the aliases(5) file is changed.  The location of the alias file is defined in smtpd.conf(5), and defaults to /etc/mail/aliases.
newaliases
```
