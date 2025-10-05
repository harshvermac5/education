https://youtu.be/Qt7l-TFBMo4

# Linux Architecture

1. Program/User
2. Shell
3. Kernel
4. Hardware

# RHEL Based Distro

1. Fedora (Run by Redhat, Community driven, Quick releases, Free, No commercial support)
2. Redhat (Run by Redhat, Corporate driven, Stable and Tested Releases, Paid commericial support)
3. CentOS (Run by community, basically Redhat without support)

# chmod

r=4
w=2
x=1
suid=4
sgid=2
sticky bit=1

Owner Group Others
rwx rwx rwx

## SUID (Set User ID)
- Allows a user to execute a file with the permissions of the file's owner

## SGID (Set Group ID)
- Executes with the permissions of the file's group

## Sticky Bit
- Restricts file deletion in shared directories — only the file's owner or root can delete.

# Linux boot process

1. BIOS/PROM
2. MBR
3. Partition Table
4. Boot Loader
5. Kernel
6. mount `/` and `/usr` in read only mode
7. checks `/etc` `/inittab` for run levels

# Run levels in Linux

1. 0: Power off
2. 1: Single user mode (text mode)
3. 2: Multiuser mode (text mode) all services except NFS and NIS
4. 3: Multiuser mode (text mode) all services enabled
5. 4: Unused
6. 5: Multiuser mode (graphics mode) all services enabled

# vi file editor

`/` is used to search for pattern


# file system operation

- `fdisk -l` : list connected disk and filesystem
- `df -h` : list connected file system
- `umount` : unmounts the file system
- `cat /etc/fstab` : list the different type of file system
- `fsck.ext4 /dev/sda1` : checks the files system

# reset the root password

1. reboot the system
2. enter kernel edit mode
3. add 1 to enter single user text only run level as shown below

`linux /vmlinuz-linux root=/dev/sda1 crashkernel=auto rhgb quiet 1`

4. `passwd root`
5. reboot

# Adding GRUB password (Legacy)

1. Generate an MD5 Password Hash and send it to grub configuration file for easier access:
`grub-md5-crypt >> /boot/grub/grub.conf`

2. Edit GRUB Configuration
`vi /boot/grub/grub.conf`

3. Add Security Lines Before Any `title` Entry:

hiddenmenu
password --md5 <hash>

```
hiddenmenu: hides the grub menu unless a key is pressed
password --md5: protects the grub entries with specified password hash
```

# Adding GRUB2 Password

1. Generate a Password Hash
Use `grub-mkpasswd-pbkdf2` to create a secure hash:
`grub-mkpasswd-pbkdf2`

2. Open the GRUB custom config file:
`sudo nano /etc/grub.d/40_custom`

Add the following lines:

set superusers="admin"
password_pbkdf2 admin grub.pbkdf2.sha512.10000.XXXXXXXXXXXXXXXXXXXXXXXX

- Replace `"admin"` with your desired username.
- Paste the full hash from step 1.

3. Update GRUB
Apply the changes:
`sudo grub-mkconfig -o /boot/grub/grub.cfg`

# Scheduling jobs

`at` command sets a job, and asks for a definite or relative time.
we can also use `at now +5 hours` to schedule a job to five hours from now.
`atq` command shows the existing jobs.
`atrm <job-id>` removes the scheduled job.
`service atd status` shows the pid of at command dameon.

`crontab -e` opens the text editor, where we can assign a task in following order:

<minutes> <hours> <day of the month> <month of the year> <day of week> <command to run>

`crontab -l` lists all the entries in crontab

`service crond status` shows the cron dameon status

# backup

`tar cvf /path/to/destination *` takes backup of all the files present in current working directory
`tar tvf backup` shows all the files present inside of backup
`tar xvf /path/to/backupfile` extracts all the information from the previously backup file

`cpio` backups takes less space than tar, we can perform cpio backup using: 
`ls | cpio -ovcf -O backup`
`cpio -itvf -I backup` shows all the backed up files
`cpio -icvf -I backup` restores the files from the backup

# SELINUX

it stands for security enhanced linux, an implementation of mandatory access contorl mechanism.
it comes in three modes

1. Enforcing
2. Permissive
3. Disabled

`gerenforce` checks the current enforcement mode
`setenforce 0` changes the mode to permissibe mode

`/etc/sysconfig/selinux` is the location of stored configuration file

# package installation

`rpm -ivh /path/to/package.rpm --force --aid` --aid flag means with all its dependencies
`rpm -Uvh /path/to/package.rpm` updates the package
`rpm -q <package-name>` checks for the installed package
`rpm -e <package-name> --nodeps` removes packages without its dependencies
`createrepo -v /path/to/repo` creates a new repo for packages installation

# file sharing

FTP is used for hetrogeneous file sharing, while NFS is used for homogeneous file sharing.

port numbers
21: ftp data
22: ftp control
2049: nfs
137: net bios name service
138: net bios datagram service
139: net bios session service

`yum install nfs*` installs all the necessary nfs file sharing utility

on server machine, check for `vi /etc/exports` and `exportfs`
above command will the show the access ip and permission

`showmount -e 192.168.80.10` checks the available mount mount, also shows the permitted ip
`mount -t nfs 192.168.80.10:/remote /nfs` if our system ip is permitted, this command will mount it in nfs directory
`vi /etc/fstab` make the necessary changes to make this mounting permanent

we can use `autofs` alternatively for automounting
autofs comes with two configuration file: `/etc/auto.master` and '/etc/auto.misc'. file auto.misc consist of network related file sharing

`yum install samba*` installs all the necessary packages related to samba
`/etc/samba/smb.conf` stores the samba configuration file
`/var/log/samba/` stores the samba logs
semi-colons `;` are used to comment the lines in samba configuration file

after editing the samba server config file, make sure to restart the service by `service smb restart`

`smbclient -L //192.168.80.10/ -N` is used to login anonymously

# DHCP server

ports
67: bootp
68: dhcp

`yum install dhcp*` will install all the dhcp related packages
`/usr/share/doc/` stores the sample configuration file
`cp /usr/share/doc/dhcp/dhcp.conf.sample /etc/dhcp/dhcpd.conf` initiates the file as usable configuration
`service dhcpd start` starts the dhcp server

# NIS server
it is a remote authentication service, essentially a client-server directory service protocols that normally used to distribute configuration data.
it works on random port number

# DNS server
Types of dns records
1. CNAME - Alias hostname
2. A - IPv4 addresses
3. AAAA - IPv6 association
4. MX - Mail exchange information
5. PTR - CNAME mapping to IPv4
6. NS - 

`named-checkconf /etc/named.conf` checks for the error in configuration file

# Apache server

`yum install http*` installs all the apache related services

# Kickstart Installation

`yum install system-config-kick*` installs all the kick-start installation files
`system-config-kickstart` now opens a gui with all the settings at one place

# sendmail
`yum install sendmail*` installs all the sendmail related packages
`/etc/mail/sendmail.mc` is the main coniguration file
`make -C /etc/mail` builds the configuration file
`/etc/mail/sendmail.cf` this configuration file is now going to be used by system
`service sendmail start` starts the sendmail service
`mail -v -s "Test Mail" steve@server.example.com` is used to send mail with specified subject line

# Logical Volume Manager

# RAID

# IPTABLES

# Virtualization

packages are avialable for 64-bit system only
```bash
yum install xen kernel-xen xen-ia64-guest-firmware virt-manager libvirt libvirt-python pyton-virtinst
```

methods:
1. Full virtualization: Hardware assisted (Kernel-based virtual machine)
2. Para virtualization: 
