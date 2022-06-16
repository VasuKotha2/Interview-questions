## Directory	Description
* /	Primary hierarchy root and root directory of the entire file system hierarchy.
* /bin	Essential command binaries that need to be available in single user mode; for all users, e.g., cat, ls, cp.
* /boot	Boot loader files, e.g., kernels, initrd.
* /dev	Device files, e.g., /dev/null , /dev/disk0 , /dev/sda1 , /dev/tty , /dev/random.
* /etc	Host-specific system-wide configuration files.
There has been controversy over the meaning of the name itself. In early versions of the UNIX Implementation Document from Bell labs, * /etc is referred to as the etcetera directory, as this directory historically held everything that did not belong elsewhere (however, the FHS restricts /etc to static configuration files and may not contain binaries). Since the publication of early documentation, the directory name has been re-explained in various ways. Recent interpretations include acronyms such as "Editable Text Configuration" or "Extended Tool Chest."

* /etc/opt	Configuration files for add-on packages that are stored in /opt .
* /etc/sgml	Configuration files, such as catalogs, for software that processes SGML.
* /etc/X11	Configuration files for the X Window System, version 11.
* /etc/xml	Configuration files, such as catalogs, for software that processes XML.
* /home	Users' home directories, containing saved files, personal settings, etc.
* /lib	Libraries essential for the binaries in /bin and /sbin .
* /lib<qual>	Alternative format essential libraries. Such directories are optional, but if they exist, they have some requirements.
* /media	Mount points for removable media such as CD-ROMs (appeared in FHS-2.3 in 2004).
*/mnt	Temporarily mounted filesystems.
* /opt	Optional application software packages.
* /proc	Virtual filesystem providing process and kernel information as files. In Linux, corresponds to a procfs mount. Generally automatically generated and populated by the system, on the fly.
* /root	Home directory for the root user.
* /run	Run-time variable data: Information about the running system since last boot, e.g., currently logged-in users and running daemons. Files under this directory must be either removed or truncated at the beginning of the boot process, but this is not necessary on systems that provide this directory as a temporary filesystem (tmpfs).
* /sbin	Essential system binaries, e.g., fsck, init, route.
* /srv	Site-specific data served by this system, such as data and scripts for web servers, data offered by FTP servers, and repositories for version control systems (appeared in FHS-2.3 in 2004).
* /sys	Contains information about devices, drivers, and some kernel features.
* /tmp	Temporary files (see also /var/tmp). Often not preserved between system reboots, and may be severely size restricted.
* /usr	Secondary hierarchy for read-only user data; contains the majority of (multi-)user utilities and applications.
* /usr/bin	Non-essential command binaries (not needed in single user mode); for all users.
* /usr/include	Standard include files.
* /usr/lib	Libraries for the binaries in /usr/bin and /usr/sbin.
* /usr/lib<qual>	Alternative format libraries, e.g. /usr/lib32 for 32-bit libraries on a 64-bit machine (optional).
* /usr/local	Tertiary hierarchy for local data, specific to this host. Typically has further subdirectories, e.g., bin , lib , share .
* /usr/sbin	Non-essential system binaries, e.g., daemons for various network-services.
* /usr/share	Architecture-independent (shared) data.
* /usr/src	Source code, e.g., the kernel source code with its header files.
* /usr/X11R6	X Window System, Version 11, Release 6 (up to FHS-2.3, optional).
* /var	Variable files—files whose content is expected to continually change during normal operation of the system—such as logs, spool files, and temporary e-mail files.
* /var/cache	Application cache data. Such data are locally generated as a result of time-consuming I/O or calculation. The application must be able to regenerate or restore the data. The cached files can be deleted without loss of data.
* /var/lib	State information. Persistent data modified by programs as they run, e.g., databases, packaging system metadata, etc.
* /var/lock	Lock files. Files keeping track of resources currently in use.
* /var/log	Log files. Various logs.
* /var/mail	Mailbox files. In some distributions, these files may be located in the deprecated /var/spool/mail .
* /var/opt	Variable data from add-on packages that are stored in /opt .
* /var/run	Run-time variable data. This directory contains system information data describing the system since it was booted.
In FHS 3.0, /var/run is replaced by /run ; a system should either continue to provide a /var/run directory, or provide a symbolic link from /var/run to /run , for backwards compatibility.

* /var/spool	Spool for tasks waiting to be processed, e.g., print queues and outgoing mail queue.
* /var/spool/mail	Deprecated location for users' mailboxes.
* /var/tmp	Temporary files to be preserved between reboots.    

## Linux system Troubleshooting - Part 1

### 1)  How to view all messages generated by the system since the last reboot on RHEL7/CentOS 7?
 * To view Linux or Unix system reboot and shutdown date and time stamp using the following commands: 
     * last command
     * who command
        * You need to use the who command, to print who is logged on. It also displays the time of last system boot. Use the last command to display system reboot and shutdown date and time, run:
        * `$ who -b`
        * `output: system boot  2017-06-20 17:41`
        * Use the last command to display listing of last logged in users and system last reboot time and date, enter:
        * `$ last reboot | less`
        * `output:`
        * `reboot   system boot  5.13.0-1029-aws  Thu Jun 16 04:50   still running  `
        Refer the below link for sample output
        * `https://www.cyberciti.biz/tips/wp-content/uploads/2006/04/last-reboot.jpg`
        Or, better try:
        * `$ last reboot | head -1`
        * `sample output: reboot   system boot  4.9.0-3-amd64    Sat Jul 15 19:19   still running` 
        For more info
        * `https://www.cyberciti.biz/tips/linux-last-reboot-time-and-date-find-out.html`
    * The last command searches back through the file `/var/log/wtmp` and displays a list of all users logged in (and out) since that file was created. 
    * utmp will give you complete picture of users logins at which terminals, logouts, system events and current status of the      system, system boot time (used by uptime) etc.
    * wtmp gives historical data of utmp.
    * btmp records only failed login attempts.
          
### 2. How to check log messages related to kernel?
* Simple answer is var/log/kern or var/log/kern.log
*  Most Important Linux Logs
* We can group most directories into one of four categories:
    * Application Logs
    * Event Logs
    * Service Logs
    * System Logs
* Critical, Must Monitor Logs
* /var/log/syslog or /var/log/messages: general messages, as well as system-related information. Essentially, this log stores all activity data across the global system. Note that activity for Redhat-based systems, such as CentOS or Rhel, are stored in messages, while Ubuntu and other Debian-based systems are stored in Syslog.
* /var/log/auth.log or /var/log/secure: store authentication logs, including both successful and failed logins and authentication methods. Again, the system type dictates where authentication logs are stored; Debian/Ubuntu information is stored in /var/log/auth.log, while Redhat/CentrOS is stored in /var/log/secure.
* /var/log/boot.log: a repository of all information related to booting and any messages logged during startup.
* /var/log/maillog or var/log/mail.log: stores all logs related to mail servers, useful when you need information about postfix, smtpd, or any email-related services running on your server.
* /var/log/kern: stores Kernel logs and warning data. This log is valuable for troubleshooting custom kernels as well.
* /var/log/dmesg: messages relating to device drivers. The command dmesg can be used to view messages in this file.
* /var/log/faillog: contains information all failed login attempts, which is useful for gaining insights on attempted security breaches, such as those attempting to hack login credentials as well as brute-force attacks.
* /var/log/cron: stores all Crond-related messages (cron jobs), such as when the cron daemon initiated a job, related failure messages, etc.
* /var/log/yum.log: if you install packages using the yum command, this log stores all related information, which can be useful in determining whether a package and all components were correctly installed.
* /var/log/httpd/: a directory containing error_log and access_log files of the Apache httpd daemon. The error_log contains all errors encountered by httpd. These errors include memory issues and other system-related errors. access_log contains a record of all requests received over HTTP.
* /var/log/mysqld.log or /var/log/mysql.log : MySQL log file that logs all debug, failure and success messages. Contains information about the starting, stopping and restarting of MySQL daemon mysqld. This is another instance where the system dictates the directory; RedHat, CentOS, Fedora, and other RedHat-based systems use /var/log/mysqld.log, while Debian/Ubuntu use the /var/log/mysql.log directory.

* A few other directories and their uses include:

* /var/log/daemon.log: tracks services running in the background that perform important tasks, but has no graphical output
* /var/log/btmp: recordings of failed login attempts
* /var/log/utmp: current login state, by user
* /var/log/wtmp: login/logout history
* /var/log/lastlog: information about the last logins for all users. This binary file can be read by command lastlog.
* /var/log/pureftp.log: runs the pureftp process that listens for FTP connections. All connections, FTP logins, and authentication failures get logged here
* /var/log/spooler: rarely used and often empty. When used, it contains messages from USENET
* /var/log/xferlog: contains all FTP file transfer sessions, including information about the file name and user initiating FTP transfers
### 3. How can you continuously monitor logs as they come in?


### 4. Where can you find messages related to the installation of Linux?

### 5. Where are most of the log files located?

## Linux system Troubleshooting - Part 2

## Kernel Parameters - Ulimit

### 6. To improve performance, how can you safely set the limit of processes for the super-user root to be unlimited?

### 7. Where can you set the resource limits for users logged in via PAM?

### 8. How to check ulimit for a user?

### 9- How to check and increase the limit of opened files in Linux?

### 10- How to view run time kernel parameters?

### 11- How to change runtime kernel parameter for maximum shared segment size in bytes?

### 12- How to view Boot time parameters and which file is modified to change these parameters?



## Linux system Troubleshooting - Part 3

## Troubleshooting with uptime lsof pidof sar and more

### 13- How to check system load without top command?

### 14- By default load average is shown in how many intervals?

### 15- How can you get the physical and virtual memory statistics?

### 16- How to check cpu utilization and other statistics?

### 17- How to find process id of a process and kill it immediatley?

### 18- How to list all open files by specified user?

### 19- How to list all open files by specified command?

### 20- How can you list all network connections by port 22?

## Advanced Linux system administrations questions and answers:



### 1-  Run a command that shows all lines except any lines starting with the a character "#" in a file?
### 2-  How can you continuously monitor log files for errors?
### 3-  How to automatically remove files older than 7 days by creating a cron job to run every night?
### 4-  How to list/print all created users on the system and send(redirect) them to a file?
### 5-  How would you list only the 2nd column from a file?
### 6-  How to broadcast a message to all logged -in users?
### 7-  How to create a user with no login access?
### 8-  How to schedule a server reboot in 15 minutes?
### 9-  How to find disk usage by the largest directories?
### 10- How to prevent users from deleting other users files in a directory?
### 11- How to display 10th line of a file only?
### 12- Your server got hacked. Due to the amount of damage, the whole server needs to be restored.How would you go about doing that?
### 13- What necessary steps should be taken to enhance the security of a server after the initial install?
### 14- Which file is the most commonly known to check for log messages?
### 15- How and why to disable ping?
### 16- Explain the different fields in /etc/passwd?
### 17- Which cammand can tell how long the system has been running?
### 18- How to check if a port is listening?
### 19- You got a ticket stating server is down, how would you troubleshoot?
### 20- How to find all files in /bin with specified(755) permissions?

## Part 2: 

### 1- What is the default port & configuration file of SSH Server ?

### 2- How to change the default ssh port in linux ?

### 3- How to change Maximum allowed sessions through SSH?

### 4- What is the configuration file of ssh client ?

### 5- How to disable SSH root login in linux server ?

### 6- How to allow only specific users to ssh your linux server ?

### 7- SCP and how its used?

### 8- How to check SSH server’s Version ?

### 9- How to setup password less ssh authentication in Linux?

## Part 3: 

### 1- How to extend SWAP space?

### 2- How to extend a logical volume?

### 3- How to create a logical volume?

### 4- How to create a volume group?

### 5- How to create a physical volume after the disk space has been added?

### 6- Is it possible to increase the logical volume on the fly?

### 7- How to reduce the logical volume and is it possible to reduce it on the fly?

### 8-9- How to scan disks for existing volume group and how to scan a logical volume from existing volume group?

### 10-11-12-13- How to activate, deactivate, disable/enable a logical volume and a volume group? How to activated the logical volume which in deactivated state? How to disable the volume group ? or Deactivate the volume group? How to enable the volume group ? or Activate the volume group?

### 14- What is the default size of a physical extent in LVM?

### 15-16-17- How to list the available logical, physical volumes and see detailed volume group info on the system?How to list the available physical volumes in LVM? How to see the detailed volume group information?

## Part 4: 

### 1- How to find files that are over 10MB in size?

### 2- How would would you run a command that shows all lines containing a character # in a file?

### 3- How would you display all lines of a file with line numbers?

### 4- How to find current system information such as the version or release info of your server?

### 5- Where are the files located for network interfaces?

### 6- Which command can you run to find if a certain package has been installed?

### 7- How to find out total lines in a file without opening that file?

### 8- How to find disk usage by the largest directories?

### 9- How to find all directories named conf under root?

### 10- How to find files not accessed in over 3 days?

### 11- How to view difference between 2 files?

### 12- What is the location of system configuration files that should be backed up regularly?

### 13- What is the command to view all the currently logged in users?

## Linux system administration Q&A

### 1- Which 2 files contain default values when creating a user with useradd command?

## Questions 2-8 covered in one lecture: 

### 2- What is the command to create a user with a pre defined uid, shell and home directory?
### 3- How to delete a user with his home directory?
### 4- How to create a user specifying a primary/Secondary grp?
### 5- How to change primary group for any user?
### 6- How can you give a normal user all the root level privileges?
### 7- How can you give sudo access to any user without asking him to provide password every time he runs a command?
### 7- How to view the User's login and logout details?
### 8- How to lock & unlock the User Account ?

## Questions 9-14 covered in one lecture: 

### 9- What is the command to view and change the expiry date for any user?
### 10- What are the fields of /etc/passwd file?
### 11- What is the difference between .bash_profile and .bashrc?
### 12- What are the details you get with finger command?
### 13- Name 3 files which are automatically created inside any user's home directory when a user is added?
### 14- What is the command to view all the currently logged in users?

## Linux basic system administration questions and answers: 

### 1- Which 2 files contain the default values when creating a user with useradd command?

## Questions 2-8 covered in part 2: 

### 2- What is the command to create a user with a pre defined uid, shell and  home directory?

### 3- How to delete a user with his home directory?

### 4- How to create a user specifying a primary/Secondary grp?

### 5- How to change primary group for any user?

### 6- How can you give a normal user all the root level privileges?

### 7- How can you give sudo access to any user without asking him to  provide password every time he runs a command?

### 7- How to view the User's login and logout details?

### 8- How to lock & unlock the User Account ?

## Questions 9-14 covered in part 3: 

### 9- What is the command to view and change the expiry date for any user?

### 10- What are the fields of /etc/passwd file?

### 11- What is the difference between .bash_profile and .bashrc?

### 12- What are the details you get with finger command?

### 13- Name 3 files which are automatically created inside any user's home directory when a user is  added?

### 14- What is the command to view all the currently logged in users?

## Linux Basic Technical questions and answers 

### How to display hidden files?

### Whats the difference between $ and # prompts on CLI?

### How to find an error in a file?

### How to make a directory?

### How to remove a directory?

### How to create a file?

### How to move a file?

### How to delete a file?

### What is the default port # for DNS

### What is the DNS package name?

### what is the configuration file for DNS and its location?

## List 3 types of file system?

### List any 4 Linux flavors?

### How to log off from Linux system?

### How to check if a package is installed?

### How to check your previously typed in commands?

### Where are zone files located for DNS?

### What is the command to find your current directory?

### How to check file permissions?

### How to find file type of a file?

### How to find where passwd command is located?

### what command is used for changing file permissions?

### What command is used to read top/bottom part of a file?

### How to check mtu, ip and MAC address?

### How to get help on certain commands?

### How to find your host name?

### How to count total lines of a file?

### What is the command to create a group?

### How to reboot a Linux machine with init command?

### Where are the user passwords saved?

### How to find running processes on your system?

### where is the network time configuration file located?

### When is the last command used?





## Student suggested Videos

### 19 new Lectures added to student suggested videos Section: 



### Boot Process RHEL/CentOS 6 and 7                                                               

### Run Levels                                                                                                            

### Targets                                                                                                                  

### NIC Bonding                                                                                                        

### What are Linux Distributions?                                                                            

### What are the advantages of using Linux?                                                        

### What is Linux?                                                                                                    

### What is a virtual environment or virtualization?                                           

### How to download and install Oracle Virtual Box?                                           

### How to download and install Redhat Linux?                                                   

### How to download, install and connect through putty?                                   

### What are different ways of accessing a Linux Server?                                     

### What is absolute vs relative Path?                                                                      

### How to Count Words, Lines and Characters in a file?                                      

### How to display and set the server's Hostname?                                              

### Explain vi editor basics?                                                                                        

### How to list and modify System Timezone?                                                       

### How to find help within Linux?                                                                            

### How to compress and archive files?                                                                  



## New Section added: "Directory structure, Files, directories, permissions and more"





### Explain Linux Directory Structure                                                                        

### What are the common file types used in Linux?                                              

### How to create files and directories?                                                                    

### How to list files and directories?                                                                            

### How to display File Contents with cat, less, more and tail?                            

### How to copy directories and files?                                                                         

### How to move or rename directories and files?                                                   
### How to remove directories and files?                                                                  

### What are the file and directory control Attributes?                                            

### Basics of File and Directory Permissions                                                               

### How to modify file permissions?                                                                            

### Explain default permissions and umask?                                                            
### How to modify file ownership and group membership?                                    

### What are special permissions: setuid, setgid and sticky bit?                             

