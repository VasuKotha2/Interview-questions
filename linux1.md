### 1. How to set a username and password to never expires
* syntax: `chage [options] username`
* Description: change user password expiry information
* Example : `chage -M -1 krishna`
  -M option used to specify the maximum and minimum number of days between password change
  -1 is used to set password to never expire

### 2. Why /etc/passwd and etc/shadow file cannot be merged into 1 file
* The existence of the two files is a consequence of that /etc/passwd is a text file that can be read by other applications (as finger, ident of ls for example), so an attacker could gain access to the information of the file that included the hashed password
* To increase the security the hashed password that used to be in the file was moved to other file called /etc/shadow that is accessible only by root

### 3. To list all the files opened by particular PID what is the command

* syntax: `lsof [option] [action or filepath]`
* Description: List open files
* Example : `lsof -p PID`
    -p option is used to List files opened by a specific process ID.

### 4. We are unable to unmount the file system. What are the reasons behind it?

* you are in the same directory (try pwd and get out of that directory if you are in same directory)
* some users are present in the directory and using its content `fuser -cu /dev/sda`
* some of the files are open in the directory `lsof /dev/sda7`

### 5. What could be the reason if server takes more time after reboot?
* filesystem got corrupt and its ext2 is not having journaling feature.

### 6. We are trying to create a file under any partition and we are getting permission denied alert. What could be the reason? However no space issue and no permission issue?
* I am running out of inode.
* Sometimes, df command reports that there is enough free space but system claims file-system is full.
* You need to check for the inode which identifies the file and its attributes on a file systems using the following command
    `$ df -i`
    `$ df -i /ftpusers/`

* Sample outputs:
 File system    Inodes    IUsed    Ifree   IUse%   Mounted on
 /dev/sda8      6250496   11568    6238928   1%    /ftpusers

* So /ftpusers has 62,50,496 total inodes but only 11,568 are used. You are free to create another 62,38,928 files on /ftpusers partition.
* If 100% of your inodes are used, try the following options:
* Find unwanted files and delete or move to another server.
* Find unwanted large files and delete or move to another server.

### 7. How to check kernel routing table information?
* There are 3 commands to check routing table information.
    `route -n`
    `netstat -rn`
    `ip route`

### 8. How to set sticky bit and what is the difference between small s and capital S?
* Sticky bit is special permission applied on a file and directory, than only root and owner of that file or directory can delete it. Even if others having full permission
* They cannot delete the file or directory
* Symbolic way: 
* `chmod o+t /opt/dump` or `chmod +t /opt/dump`
* Numerical way:
* `chmod 1757 /opt/dump/`   
* To make this setuid executable you have to say,
* `chmod 4700 executable`
* Also,
* `s - setuid and executable`
* `S - setuid and not-executable`

### 9. Which file is used to specify default gateway?
* `/etc/sysconfig/network`

### 10. In RHEL 7, how to switch between two runlevels?
* `systemctl isolate multi-user.target`
* `systemctl isolate runlevel3.target`
* Changing the default runlevel
* `systemctl set-default multiuser.target`
* `systemctl get-default`
