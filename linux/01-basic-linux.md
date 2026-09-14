# Basic Information, History & Distributions

## What is Linux?
```text
Linux is an open-source, Unix-like operating system kernel that manages hardware resources and provides a foundation for operating systems and applications created by Linus Torvalds in 1991.

Therefore, terms such as Ubuntu, Debian, Fedora, Rocky Linux, Arch Linux, etc. are called Linux distributions (distros).
```

## What is a Kernel?
```text
The kernel is the core component of an operating system.
It works as a bridge between:

Applications
     ↓
Linux Kernel
     ↓
Hardware (CPU / RAM / Disk / Network)

The kernel manages:

- CPU
- RAM
- Processes
- Filesystems
- Networking
- Devices
- Security
- Hardware communication
```

## History of Linux

### UNIX
```text
Before Linux, UNIX was one of the most influential operating systems in computing history.

UNIX was developed at AT&T Bell Labs in the late 1960s and early 1970s.

Important UNIX developers included:

- Ken Thompson
- Dennis Ritchie
- Brian Kernighan

Dennis Ritchie also created the C programming language, which became extremely important for operating-system development.
```

### MINIX
```text
In 1987, Andrew S. Tanenbaum created MINIX.

MINIX was a small Unix-like operating system primarily designed for education.

It influenced Linus Torvalds while he was studying computer science at the University of Helsinki.
```

### Linux Creation
```text
In 1991, Linus Torvalds started developing a new Unix-like kernel.

On August 25, 1991, he announced his project to the MINIX newsgroup.

The original project was initially developed for the Intel 80386 processor architecture.

Linux was initially a personal project, but developers around the world began contributing to it
```

### Linux and GNU
```text
Linux became especially powerful when combined with the GNU project.

The GNU Project was started by Richard Stallman in 1983.

GNU provided many important components, including:

- GNU Compiler Collection (GCC)
- GNU Core Utilities
- GNU Bash
- GNU C Library
- GNU development tools
```

### Open Source and Linux
```text
Linux is open-source software.

The Linux kernel is released under the GNU General Public License version 2 (GPLv2).

This allows developers to:

- Study the source code
- Modify the source code
- Distribute copies
- Contribute improvements

This open development model helped Linux grow into a global project.
```

### Major Linux History Timeline
```text
Year	Event
1969	UNIX development begins at Bell Labs
1971	Early UNIX versions developed
1973	UNIX largely rewritten in C
1983	GNU Project started by Richard Stallman
1987	MINIX released by Andrew Tanenbaum
1991	Linus Torvalds starts Linux development
1991	First public Linux announcement
1992	Linux adopts GPL license
1993	Debian project started
1993	Slackware released
1994	First stable Linux kernel 1.0
1995	Red Hat Linux released
2004	Ubuntu first released
2010s	Linux becomes dominant in cloud/server infrastructure
2020s	Linux widely used in cloud, containers, Kubernetes, AI and embedded systems
```

### What is a Linux Distribution?
```text
A Linux distribution is a complete operating-system package built around the Linux kernel.
```

### Major Linux Distribution Families
```text
Linux Distributions 
│ 
├── Debian Family 
│   ├── Debian 
│   ├── Ubuntu 
│   ├── Linux Mint 
│   └── Kali Linux 
│
├── Red Hat Family 
│   ├── RHEL 
│   ├── Fedora 
│   ├── Rocky Linux 
│   └── AlmaLinux 
│ 
├── Arch Family 
│   ├── Arch Linux 
│   ├── Manjaro 
│   └── EndeavourOS 
│ 
├── SUSE Family 
│   ├── openSUSE 
│   └── SUSE Linux Enterprise 
│   
└── Independent / Other 
    ├── Alpine Linux 
    ├── Gentoo 
    └── Slackware
```

## Debian Family

### Debian
```text
Debian is one of the oldest and most influential Linux distributions.

It was founded by Ian Murdock in 1993.

Characteristics:

- Stable
- Community-driven
- Large software repository
- Excellent server distribution
- Uses .deb packages
- Uses APT package management

Common commands:

sudo apt update
sudo apt upgrade
sudo apt install nginx
sudo apt remove nginx
```

### Ubuntu
```text
Ubuntu is based on Debian and is developed by Canonical.

Ubuntu is extremely popular for:

- Cloud servers
- DevOps
- Software development
- Docker
- Kubernetes
- Web servers
- Desktop environments

Examples:

Ubuntu Desktop
Ubuntu Server
Ubuntu Cloud

Package management:

apt

Package format:

.deb

Example:

sudo apt update
sudo apt install nginx
```

### Kali Linux
```text
Kali Linux is Debian-based and designed primarily for:

- Cybersecurity
- Penetration testing
- Digital forensics
- Security research

It includes many security-related tools.

Kali should not normally be treated as a general-purpose production server distribution.
```

## Major Package Managers
```text

Debian / Ubuntu
apt
Example:
sudo apt update
sudo apt install nginx

RHEL / Fedora / Rocky / AlmaLinux
dnf
Example:
sudo dnf install nginx

Arch
pacman
Example:
sudo pacman -S nginx

Alpine
apk
Example:
apk add nginx

SUSE
zypper
Example:
sudo zypper install nginx
```

### Linux Shell
```text
A shell is a program that allows users to interact with the operating system.

Example:

User
 ↓
Shell
 ↓
Kernel
 ↓
Hardware

Popular shells include:

- Bash
- Zsh
- Fish
- Ksh

The most common shell in Linux administration is Bash.

Example:

echo "Hello Linux"
```

### Linux Terminal
```text
The terminal provides an interface for interacting with the shell.

Example:

ls
cd /var/log
pwd
mkdir test

A terminal itself is not the shell.

The relationship is approximately:

Terminal Emulator
       ↓
Shell
       ↓
Commands / Programs
       ↓
Linux Kernel
```


### Linux Filesystem
```text
Linux uses a hierarchical filesystem.

The top-level directory is:

/

This is called the root directory.

Typical structure:


Directory	Purpose
/	    Root of filesystem
/home	Normal users' home directories
/root	Root user's home
/etc	Configuration files
/var	Variable data and logs
/tmp	Temporary files
/usr	User-space programs and libraries
/opt	Optional/third-party software
/dev	Device files
/proc	Process/kernel information
/sys	Kernel/device information
/boot	Boot-related files
```

## Linux Architecture
```text
A simplified Linux architecture looks like this:

+----------------------------------+
|          Applications            |
| Laravel | Nginx | MySQL | Docker|
+----------------------------------+
                ↓
+----------------------------------+
|       Shell / System Tools       |
| Bash | systemctl | ip | ps | ls |
+----------------------------------+
                ↓
+----------------------------------+
|          System Libraries        |
|              glibc               |
+----------------------------------+
                ↓
+----------------------------------+
|          Linux Kernel            |
| Process | Memory | Network       |
| Filesystem | Device | Security   |
+----------------------------------+
                ↓
+----------------------------------+
|             Hardware             |
| CPU | RAM | Disk | NIC | Devices |
+----------------------------------+
```

## Linux Users
```text
Linux is a multi-user operating system.

A system can contain multiple users:

root
developer
deploy
ubuntu
admin

View the current user:

whoami

View logged-in users:

who
```

## Root User
```text
The root user has extremely powerful privileges.

Example:

sudo systemctl restart nginx

sudo allows an authorized user to execute a command with elevated privileges.

Avoid using root unnecessarily because mistakes can damage the system.
```

## Linux Permissions
```text
Linux uses permissions to control access.

Example:

-rwxr-xr--

Three major permission categories are:

User
Group
Others

Three common permissions are:

r = read
w = write
x = execute

Example:

chmod 755 script.sh

Ownership:

chown user:group file.txt
```

## Linux Networking
```text
Linux provides powerful networking capabilities.

Common commands include:

ip addr
ip route
ping
ss
curl
wget
dig
nslookup
traceroute

Example:

ip addr

shows network interfaces and IP addresses.

Example:

ss -tulpn

shows listening network sockets.
```


