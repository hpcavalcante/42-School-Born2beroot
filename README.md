# Born2beroot
In this project we have to create our own virtual machine and set up as a server by following specific rules. 

You must choose as an operating system either the latest stable version of Debian (no
testing/unstable), or the latest stable version of CentOS.

In my case I choose Debian.

## Mandatory:
> 1. Choose between two Linux-based distribuitions: `CentOs` or `Debian`.
> 2. Create and understand the concept about `LVM` partitions and encrypted partitions (For the mandatory part we have to create at least 2 ecrypted partitions using LVM).
> 3. Install and configure `SSH services` for running on specific ports.
> 4. Configure `UFW firewall` to allow only specifics connections to your server.
> 5. Set-up hostnome and a strong password policy for users.
> 6. Install and configure `sudo` to specific users.
> 7. Create a monitoring script, that displays specific information about your server every 10 minutes.

## Bonus part:
> 1. Set-up a different layout of partitioning, more partitions are required for this part (as well as more disk space).
> 2. Set-up a functional `WordPress` website with the guidelines provided.
> 3. Set-up a webserver service of your choice and justify.

## Concepts

This project requires the student to configure a working virtual machine to serve as a server. There are many step by step tutorials on the internet for this. In my case I chose to focus only on the concepts of this project with brief explanations. To really understand these concepts, start here and look for more information.

## Index
- [Born2beroot](#born2beroot)
  - [Mandatory:](#mandatory)
  - [Bonus part:](#bonus-part)
  - [Concepts](#concepts)
  - [Index](#index)
    - [How virtual machine works](#how-virtual-machine-works)
    - [The choose of operational system](#the-choose-of-operational-system)
    - [CentOS/Debian](#centosdebian)
    - [The purpose of virtual machines](#the-purpose-of-virtual-machines)
    - [APT/Aptitude](#aptaptitude)
    - [APPArmor](#apparmor)
    - [How to check services status](#how-to-check-services-status)
    - [Users and groups](#users-and-groups)
    - [Passwords security](#passwords-security)
    - [Hostname](#hostname)
    - [Partitions and LVM](#partitions-and-lvm)
    - [SUDO](#sudo)
    - [SSH](#ssh)
    - [UFW](#ufw)
    - [CRON](#cron)
    - [SCRIPT](#script)

### How virtual machine works
> A virtual machine allows your system to run a entire operational system inside your host OS. The hypervisor is responsible to manage and share the resources of your physical machine beetwen your host OS and your virtual machines.

### The choose of operational system
> In my case I chose Debian. I made this preference for Debian because I already have some experience with the system and because of its large community. If a problem arose during the project, it would be much easier to find help. You have to justify your choice of operating system.

### CentOS/Debian
> Debian is a general purpose system, while CentOS is built for corporate use. Because of this difference, there are many more packages available on Debian servers than on CentOS. There are several other small differences, like the package manager, APT for Debian and YUM for CentOS, the configuration files are also in different places, default programs are different and so on...

### The purpose of virtual machines
> Virtual machines can be used for more than one purpose, such as creating servers. Servers usually don't require a lot of resources to run, so you can create many servers on one machine using virtual machines. Other common uses for VM's are to safely test some application, running an application in your virtual machine is safe because a virtual machine doesn't have a direct connection to your physical machine so you can literally wreck your system in a VM and not do any damage to your host system.

### APT/Aptitude
> Both are package managers. Apt is Debian's default package manager. With it you can remove, search, install, update and configure packages on your system. apt is a CLI, ie it works from the command line and obeys user-defined rules about what it should do and how to do it. Aptitude works in the same way as apt but uses a graphical interface, making it more friendly and easier to manage the system's packages, it can be very useful for those who don't have much experience with the package manager and don't know how to find certain settings and in some other cases.

### APPArmor
> It is a kernel security layer responsible for managing permissions for applications in terms of the use of machine resources. Like network access, permition to write, read or execute in disk and access of the general resources of the machine. 

### How to check services status
> To check the status of a service on Debian, we can run the command `sudo systemctl status <nameofservice>`. The `systemctl` command is a handler for systemd, which is a handler for almost everything on Linux. We can check service status, stop services from running, start services and use for many other things.

### Users and groups
> Your user must be your intra login and belong to sudo and user42 groups.
> Some useful commands to do that:
> - `sudo adduser <newusername>` - Creates a new user.
> - `sudo addgroup <newgroupname>` - Creates a new group 
> - To add a user in a group we can use the command `adduser` with addition of the group we desire to add this user. Like `sudo adduser <username> <groupname>`
> - `groups <username>` - Shows all the groups the user belong
> - To check all users in system we can use `cat /etc/passwd`

### Passwords security
> Passwords in this project must follow strict rules. For this we must install the package called pwquality (`sudo apt install libpwquality-common`), which allows us to define some rules for creating passwords. And we have to edit the `/etc/login.defs` file to define password expiration rules. After installing pwquality we have to edit the configuration file in `/etc/security/pwquality.conf`.

### Hostname
> Hostname is the name of machine in our network. In subject is required to hostname is your intra login + 42 (e.g: intralogin42)

### Partitions and LVM
> The name is an acronym for logical volume manager. And this volume manager allows greater flexibility when creating partitions (logical volumes) and managing them. System admin can easily manage free space from one volume to another as needed, add new physical volumes to a logical volume group and increase their capacity without formatting and losing data.

### SUDO
> In this project we will have to create specific rules for the use of SUDO. Sudo is a program that allows an ordinary user to have superuser (root) powers for a certain period of time. So the system admin can manage user permissions more securely, giving this power or taking it away. Rules for sudo can be defined in a new file created in `/etc/sudoers.d/`. As the project asks, create a log file in `/var/log/sudo/`. The path to this file must be specified in the configuration file created earlier. We must also add the user created during the evaluation to the sudo group, so that he also has the permission to use SUDO and have root powers. (e.g sudo adduser user sudo).

### SSH
> Security protocol that allows data exchange between server and client using a simple and secure connection. It prevents the data exchanged between the parties from being exposed or corrupted by third parties. Using an encryption method making it possible to access this data only by the authorized client and server. We have to be sure that the only port used for ssh conections is the 4242 port, to do that we can verify and edit it in `/etc/ssh/sshd_config`.

### UFW
> UFW is simply the system's firewall, it allows the creation of incoming and outgoing rules over the network. It is through it that we will configure the system to allow the only way to access the system through the network is through port 4242.

### CRON
> It is a task scheduler that allows you to schedule tasks to run in a certain period of time. It is important to know that cron creates different profiles for each user. We can edit the current user's profile via `crontab -e`.

### SCRIPT
> Using the system's own command output and some log files, you can create a shell script with outputs using `echo`. It is also important that you "format" these outputs to show only what was requested by the pdf. Redirections through the pipe "|" for commands like `awk` can be useful to do this.