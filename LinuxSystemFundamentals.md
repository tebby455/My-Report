![Linux](images/linux.png)
# Linux System Fundamentals
<p> Nowadays, Linux (an operating system distributed under an open-source license) is becoming popular for providing a platform which developers could intervention to a system, a network server. Almost IT professionals with or no Linux experience they can be approached to. Linux provides a role better than other OS like Organizing, Managing and Operating a server, also services in Information Systems, secure for environment, solutions, ... for personal, organization and enterprise, ... Here is my report for basic and fundamentals in Linux.
</p>

***

## Outline 

<a href='#Section1' style='text-decoration: none'>I. Linux Session</a>

<a href='#Section2' style='text-decoration: none'>II. Process Control</a>

<a href='#Section3' style='text-decoration: none'>III. Basic Command line with Linux</a>

<a href='#Section4' style='text-decoration: none'>IV. Text Editing Tools</a>

<a href='#Section5' style='text-decoration: none'>V. I/O Redirection</a>

<a href='#Section6' style='text-decoration: none'>VI. Filters</a>

<a href='#Section7' style='text-decoration: none'>VII. File Links</a>

<a href='#Section8' style='text-decoration: none'>VIII. Basic Tool for Network</a>
***

<div id='Section1'></div>
#### I. Linux Session

1. **Checking Information of a Linux system**

	- Checking information of a system is a important thing you have to know, specially when you are working with server. More information you know, more success you work for your project.

	a. Checking CPU: By default in Linux OS, you can check CPU Information by `lscpu` command.
		![lscpu](images/Information/lscpu.png)

	b. Checking RAM: to check memory for easy working, running suitable program, avoid unecessary program, for developers, they have to consider for coding.
  	- 1. Using `free [OPTION]`

		* Ex: use `free` for normally checking RAM

			![free](images/Information/free.png)
		* [OPTION]: In this common command [OPTION] are used is defind output in specific unit (`-k` kilobytes, `--mega` megabytes, ...)
		* Other, there is command `free -t` to show all memory(RAM) and swap.

	- 2. Using `cat /proc/meminfo`: This is command to show full detail of Memory information.

	c. Checking network: to check network interface, also IP, subnet mask, gateway, broadcast, ...

	- Basically checking network by `ifconfig` if you installed **net-tools**, if not use `ip a` means **ip address**

		* `ip a`

		![ipa](images/Information/ipa.png)

		* `ifconfig`

		![ifconfig](images/Information/ifconfig.png)

	- `netstat [OPTIONS] <socket>` 

		* Tool for follow all of network connection output and input in system. It is useful for solving problem in network. 
		* Common [OPTIONs]:

			* -r: show routing table
			* -i: show interface table
			* -o: display timers
			* -a: show all sockets

			![netstat](images/Information/netstat.png)

	- `traceroute [IP]` 

		* Print the route packets trace to network host

			![traceroute](images/Information/traceroute.png)

	- `ping [IP]`

		* `ping` sned ICMP ECHO_REQUEST to network host, it uses to check the network, or connection from source to dest.

			![ping](images/Information/ping.png)

	- `vnstat` 

		* `vnstat` use to check bandwidth and packet rate of network card.

			![vnstat](images/Information/vnstat.png)
			> command _-l_ to show in real time, _-i_ to choose interface, you can check in _ifconfig_
2. **Users and access permission of users**

	- ***Users***: There are accounts that you create in Linux, it relates to use ***_username_*** and ***_userID_***

		* ***Username***: It often uses to login, provide permission, ... but in Linux, system works in ***UserID***
		* ***UserID***(User identifier): A number go with ***username***, OS uses this number to manage.If two users have different name but have the same UID, these are still in one user. In Linux, to check UID, it stores in ***/etc/passwd***, use `cat /etc/passwd`

			![Output of UID](/images/User/uid.jpg)
			
	- ***Access Permission***: In Linux, permission of users divide into 2 permission:

		* ***root***: If users have ***root*** permission, those users can be accessed anything in system. These are called ***superuser***, have an userUID=0.
		* ***normal***: It means that users have userUID#0, oftenly users that clients create a new user in system. These are work in permission of ***user with root permission***. 

3. ___Checking current Disk usage *df command*___
  a. ***df*** command
    - Showing the amount of disk space used and size available on Linux file System.   
    
 	 b. ***Syntax***: df [OPTION] ... [FILE] ...
  	- ***Example***: 
      * Show all of current disk in System: `df [Enter]`
      * Show a specific file/folders: `df -a /dev/sdb1`: there is will show | Filesystem | 1K-blocks | Used | Available | Use% | Mounted on.
    - [FILE]: Like in Example, my file is ***/dev/sdb1***
    - ***Common*** [OPTION]:
      * -a, --all: show all file systems, include hidden files.
      * -h: show block Size in power of 1024 (ex: 1024M)
      * -H: show block Size in power of 1000 (ex: 1.1G)
      * --total: show a sum of all of disk (ex: I have 2 disk 100G of each, there is will show a line total is 200G)
      * -T: show a file Type (ex: I partition disk to store data is /dev/sda4, it is ***a ext4 type***
3. ___Checking summarize disk usage of the set of FILEs *du command*___
	a. ***du command***
    	- Showing disk usage then estimate for space usage. For example: I have disk A with size is 100GB, I use command, it shows that my Disk A used 2GB, for that I               could estimate space usage of Disk A.  
  	b. ***Syntax***: du [OPTION] ... [FILE] ... (recommended to use)
    or: du [OPTION] ... --file0-from=F
    - ***Example***: 
      * When you are in specific folder, ex., you are in ***_/home/name/Downloads_***
      * Use: `du [ENTER]`, there will show all of file that folder contains and their size
      * `du -a _/home/name/Downloads_`: show all of file and size that you choose, in here I choose check in _/home/name/Downloads
      * `du -a _--file-from=/dev/sdb1_`: summarize disk usage of the Disk, in here I check in disk _/dev/sdb1_.

	- ***Common*** [OPTION]:

	* -a, -all: show all file in directory
	* -h: show size of files that human readable format (ex: 1K, 1M, 1G,...)
	* -c: show total size file in directoryrecursively
	* -d + [number]: show the total level for a directory (ex: my [number] is 1, I am in ***/home/name***, it will show ***/home/name/Downloads***, if number is 2 it shows ***/home/name/Downloads*** and ***/home/name/Downloads/Telegram***)
	* -s: show only total of directory

4. **Checking Disk Partition**

	a. ***fdisk*** command
	
	- **fdisk** is the most common used command to check the partitions on the disk. It displays the partition and details like file system type, but it does not report size in unit of each partitions. Other, **fdisk** can be used in partition disk or change many thing on disk.
	- **Syntax** 

		* `fdisk [OPTION] <disk>` change, edit partition disk
		* `fdisk [OPTION] -l <disk>` list partition table of disk
			![fdisk](images/Disk/fdisk.png)
			> This is command for show all of partition of disk that are in your computer
		* If you want to show specific of disk, ex: `fdisk -l /dev/sda1`

	b. **`df command`** this command can be used to check partition 
		![df command](images/Disk/df.png)

	c. Mount and Umount

	- **Mount:** Allow computer access to I/O storage device like USB and hard drive. 

		* __Syntax__: `mount [OPTIONS] device dir` or `mount [OPTIONS] device|dir`
		* Common [OPTIONS]

           * -l: List all the file systems mounted file
           * -h: help, display full options
           * -V: show version of `mount`
           * -a: mount all filesystems mentioned in fstab
           * -t: type of filesystem device uses
           * -r: set read-only to file mounted

		* Example: `mount -l -t ext4` to list all mounted file that are using type **ext4**

			![mount](images/Disk/mount.png)

	- **Umount:** When you finish working with any divice that you mounted, you have to umount it to avoid data missing.

		* __Syntax__: `umount [OPTIONS] <source> | <directory>`
		* Common [OPTIONS]

			* -a: unmount all filesystems
			* -r: if unmounting fail, that disk will be remount in read-only
			* -t: tyoe of filesystem device uses
			* -f: force to unmount

		* Example: `mount /media/dirname`, if output does not appear anything, it success.
			![umount](images/Disk/umount.png)

_ _ _

<div id='Section2'></div>
### II. Process Control

1. **Overview**

	- Process control is a technical to follow time by time the process activities. Managing and resolving problems in operation of process. In each processes, these are have Process ID(PID). There are two type of process: **Foreground Process** and **Background Process**

		* __Foreground Process:__ Every processes that you run interactively in your shell are Foreground Process. If a process have a while to run, you have to wait and cannot do anything until it finishs or you interupt it by `CTRL Z`. Example: I `ping 8.8.8.8`, it will run after 5 times ping _icmp_seq_ for Windows, for Linux it will continue until you `CTRL Z`, in while it is running you cannot do anything.
		* __Background Process:__ Every processes that you run, it does not interact with your shell directly. You can run other process while Background Processes are running. Example: I run `sudo`, it will run in system, to stop it `exit`

			![example](images/process/example.png)

2. **Viewing process status __`top`__**

	- In Linux, to display all process in real-time view of a running system, use `top`. It could be display system summary information as well as list of processes or threads.
	- __Syntax:__ `top [OPTIONS]`

		* Common [OPTIONS]: 

			* -e: k(kilobytes) | m(megabytes) | g(gigabytes) | t(terabytes) | p(pebibytes): Enfoce task memory scaling
			* -E: k(kilobytes) | m(megabytes) | g(gigabytes) | t(terabytes) | p(pebibytes): Enfoce sumary memory scaling
			* -s: use in secure mode

		![top](images/process/top.png)
		> PID: process id
		> PR: priority of the task
		> NI: Nice Value of task, positive NI means lower priority, negative means higher priority
		> VIRT: virutal memory used
		> SHR: shared memory size
3. **Kill a process**

	- `kill <PID>` when you install a tool, but it has conflict with PID(ex: PID=111), so you have to kill it if it does not affect with running system.
	-  Example: kill a process with PID is 10, `kill -9 10`, _-9_ is shutdown immediately.
___

<div id='Section3'></div>
### III. Basic command line with Linux

1. **Working with directories**

	a. __`pwd`__

	- `pwd` print name of current/working directory. For the old Linux OS, this command was helpful for people who working in Linux.

		![pwd](images/command/directory/pwd.png)
		> Common used in _pwd_

	b. __`cd`__

	- `cd` change your current direcotry to _/root_ directory

		![cd](images/command/directory/cd.png)

	- More options in cd: 

		* __Syntax:__ `cd <path dir>`
		* `cd ..` go to the parent directory
		* `cd -` go to previous directory

	c. __`ls`__
	- `ls` list the content of a directory
	- __Syntax:__ `ls [OPTIONS] <path dir>`

		* By default, use _ls_ for current directory, if you want to list other directory, you can use `ls [OPTION] <path dir>`, ex: `ls -a /home/huynx/Desktop`
		![ex-ls](images/command/directory/ex-ls.png)

		* Common [OPTIONS]

			* -a: to show all hidden files
			* -l: to display the content in different format
			* -h: to show the number of size in human readable format

			![compare without options and with option -l](images/command/directory/compare.png)
			> Different between _ls_ and _ls -l_

	d. __`mkdir`__

	- `mkdir` to create a new directory. Common used to create `mkdir mydir`
	- __Syntax:__ `mkdir [OPTIONS] dirname`
	- Common [OPTIONS]:

		* -p: to create a parent directory, for example: `mkdir -p mydir1/mydir2/mydir3` it will be created _mydir1_ then _mydir2_ in _mydir1_, ... 

			![mkdir -p](images/command/directory/mkdir-p.png)

	e. __`rmdir`__

	- `rmdir` to delete direcoties if they are empty
	- Example: I used `rmdir` to delete ***mydir*** that I created before

		![rmdir](images/command/directory/rmdir.png)
		> I can not delete because in _mydir_ it has other directories

	- In order to delete by `rmdir`, also use `rm (remove dir)` it can deleted directories that have content inside and common [OPTIONS] is `-rf`

2. **Working with files**

- Directories is a special kind of file. 
	a. __`locate`__

	- `locate` to search a file, or search by file type
	- Basically, search a file without any options `locate task.txt`

		![locate](images/command/file/locate.png)

	- If you do not remember name of file, just know file type, use `locate *.txt`, this command show all file with type is _.txt_

	b. __`cp`__

	- `cp` to copy file(s)
	- **Syntax:** `cp [OPTIONS] SOURCE DEST `, copy SOURCE to DEST or multiple SOURCE to DEST

		* In current directory, I copy a file into two, `cp hello.txt hello1.txt`

			![copy](images/command/file/cp.png)

		* Copy a file forward to another directory, `cp hello.txt /home/name/Desktop/hello.txt`
		* To copy multiple SOURCE to DEST, `cp task1 task2 task3 /home/name/Desktop/`, last argument must be a dricetory
		* -i: if you want to overwrite file that existing

	- Do the same with directories

	c. __`mv`__

    -  `mv` to move file(s)
	- **Syntax:** `mv [OPTIONS] SOURCE DEST/DIR `, rename SOURCE to DEST or move SOURCE to DIR

		* Can rename with `mv`, `mv hello.txt aloha.txt`

			![mv-rename](images/command/file/mv-rename.png)

		* To move a file `mv aloha.txt 
			![mv-move](images/command/file/mv-move.png)

	- __`zip and unzip`__

		* `zip` is used to pack files into 1 file with smaller size. In Linux, there are many type of zip, **tar, gzip, zip, bz, 7z, ...**

			1. `tar`

				- `tar` a tool zip popular in Linux, last of files have `.tar`
				- **Syntax** `tar [OPTIONS] file`

					* Common [OPTIONS]

						* -cvf: to create a storage file, locate to it then pack, show working on screen
						* -cvzf: the same but work with only `.gz`, common use in file has `.tar.gz`

			2. `gzip`

				- **Syntax** `gzip [OPTIONS] filename`

					* Common [OPTIONS] 

						* -1~9: level for zip
						* -l: check attribute file zip

		* `unzip` to unpack file zipped

			1. `tar`

				- **Syntax** 

					* -xvf: create a storage then unpack in there.
					* -xvzf: the same but in `.gz`

            2. `gzip`

				- **Syntax** `gzip [OPTIONS] filename`

					* Common [OPTIONS] 

						* -1~9: level for zip
						* -l: check attribute file zip

1. **Working with file contents**

	a. __`head`__ 

	- `head` to display first ten lines of a file

		![head](images/command/file/head.png)

	- If you add _-[number line]_ `head -4 task.txt` there will show first 4 lines.

	b. __`tail`__
	- `tail` to display last ten lines of a file

		![tail](images/command/file/tail.png)

	- If you add _-[number line]_ `head -4 task.txt` there will show last 4 lines.

	c. __`cat`__

	- `cat` command is one of the most universal tools. It uses display a file on the screen without editor.
		![cat](images/command/file/cat.png)

	- `cat` also to use create files, `cat > hello.txt`

	d. __`more and less`__

	- `more and less` used to display file that take up more than one screen like your screen not enough to contain all of content. Users use space bar to see the next page, **q** to quit. `more and less` are the same uses but lightly different format.

		![more](images/command/file/more.png)

	___

<div id='Section4'></div>
## IV. Text Editing Tools
   - In Linux, almost Text Editor can be used for developer, coding with better efficiency than compiler.


1. **Vim Editor**(best for Ubuntu)

    - **Vim editor** a tools famous in text editor with many shortcut keys, running fast, but not easy to use for beginers. 
    - To run **vim**, `vim`, run it with create a file `vim hello.txt`

2. **Vi Editor**(most primitive editors in Linux)

	- To run *vi editor*, `vi`, or create a file `vi hello.txt`
	- _vi_ have 2 basics mode: _insert_(allow user can write), _command_(user only use commands in this mode)
	- There is some commands that useful for use _vi_:

		* :w	Write this file out
		* :q	Quit _vi_ w/o writing
		* :q!	Force quit _vi_ w/o writing
		* :w!	Force write
		* :wq	Write then quit

3. **Nano GNU Editor**

	- This is a text editor which for users easy to use, also popular in Unix and Linux.
	- To run _nano_, `nano`, to create a file `nano hello.txt`

		![nano](images/text-editor/nano.png)

___

<div id='Section5'></div>
## V. I/O Redirection

- In the bash shell has three standard stream: **stdin(standard input)**, **stdout(standard output)**, **stderr(standard error)** 

	![topology](images/IOredirect/model.png)


1. __`dev/null`__

   -  `dev/null` is a virtual file. Everything you stored in `dev/null` is useless, it will be removed. A null device, it received anything you redirect to
2. ___Standard Input(stdin)___

	- Standard Input is a stream which a program *read* its input data, default stream = 0. It is request data by use of the *read* operation.
	- Example: `cat /etc/passwd`, if you use `cat` without any parameter or option, it will slient execute with any input from keyboard until **CTRL D(Character EOF)**
	- For redirection, standard input is inherited from the parent process.

		![stdin](images/IOredirect/stdin.png)

	- Redirect Standard Input `<`

		* Using to read data from a file, then use it to input from another file.

			![redirect standard input](images/IOredirect/redirectinput.png)

3. __Standard Output(stdout)__

	- Standard Output is a stream which a program *writes* its output data, default stream = 1. It is request data by use of the *write* operation, example `cat hello.txt`

		![stdout](images/IOredirect/stdout.png)

	- Redirect Standard Output

		* `1 > file`: redirect output to file, overwrite to file

		* Example: `echo hello > hello.txt`
4. __Standard Error(stderr)__

	- Standard error is another output stream, used by program to output *error messsages*. It is a stream independent of standard output can be redirected separately. Default stream = 2.

		![error](images/IOredirect/error.png)
	
	- Redirect Standard Error

		* `2 > file`: use to prevent error messages from cuttering your screen

			![redirect standard error](images/IOredirect/redirecterror.png)

5. __`>> append to file`__

	- `>>` is a operator which is adding content into the last content of file.

		![append](images/IOredirect/append.png)

6. __`pipe`__

	- Basically, `pipe` is a type of redirecting, use output of program  then redirect to input of another program.
	- Signal: `|`

		![pipe](images/IOredirect/pipe.png)

___

<div id='Section6'></div>
### VI. Filters

1. __`tee`__

	- `tee` put **stdin** and **stdout** into a file. Function `tee` is same `cat`. Sometime, we can use `-a` append to file.

		![tee](images/filter/tee.png)

2. __`grep`__

	- `grep`, common use is to filter lines of text containing. There are many [OPTIONS] of `grep` for regular expressions.

		![grep](images/filter/grep.png)
		> Instead of I use _grep copy_, I can use _grep -i copy_ means ignore case

3. __`cut`__

	- `cut` can select columns from files.

		![cut](images/filter/cut.png)

4. __`tr`__

	- `tr` can translate character.

		![tr](images/filter/tr.png)

5. __`wc`__

	- `wc`, counting words from a file.

		![wc](images/filter/wc.png)

6. __`sort`__

	- `sort` will filter file by default to an alphabetical sort.

		![sort](images/filter/sort.png)

7. __`uniq`__

	- `uniq` remove duplicates from a sorted list

		![uniq](images/filter/uniq.png)

8. __`sed`__

	- `sed` basic workflow is Read, Execute, Display, it often uses to filter by use regular expression.

___

<div id='Section7'></div>
### VII. File Links

1. **Hard Links**

	- When you create a **hard link** to a file win `ln`, an extra entry is added in the directory.

		![hardlink](images/file_link/hardlink.png)

	- `ln` is a tool for create a files system to only an app with diferrent structure for efficient.

2. **Symbolic Links**

	- **Symbolic links** is a special file point to another directory, it called **target**. When its created, it can be replaced instead **target**. It is unique and can be placed anywhere you want. 1 target can be pointed to many symbolic links.

		![symbolic links](images/file_link/symlink.png)

___

<div id='Section8'></div>
### VIII. Basic Linux Tool

1. ***nmap tool***

	- `nmap` is a open-source port scanner for UNIX and Windows. It supports a wide variety of scan types. Providing to assist users of nmap in scaning own network, or network has been given permission, also to determine the security of network. It also a Network exploration tool and security/ port scanner.
	- **Syntax** `nmap [Scan types] [OPTIONS] <target IP or DNS>

		* Common [Scantype] [OPTION]: 

			* -sn: ping scan withour port
			* Scan techniques: -sS/sT/sA/sW/sM: TCP SYN/Connect()/ACK/Window/Mainmon scan
			* -sU: UDP scan
			* -sV: probe open ports to determone serivce/version
			* -sC: script scan

			![scan](images/basic_tool/nmap/scan.png)

2. __`git`__

	- Git is a version-control system for tracking changes in computer files and coordinating work on those files among multiple people. Gis is a ***Distributed Version Control System***. 

		![workflow](images/basic_tool/git/workflow.png)

	- Common Command Line in GIT:

		* `git add`: to add file that is in the working directory
		* `git commit`: to add all files that are staged to the local repository
		* `git push`: add all file in the local repository to GitHub.
		* `git clone`: to Download a repository of someone in GitHub.

3. **Telnet**

	- A protocol to remote access to another PC, Router,... Telnet protocol, is used popular in local, because it does not have security, so that it connects fast.
  
		![telnet](images/basic_tool/telnet.png)

4. **Secure Shell(SSH)**

	- A protocol allow user can remote access to another computer in Internet. It has security, encode passwd, so that connect lower than Telnet

		![ssh](images/basic_tool/ssh.png)

	- **generate ssh-key***

		* use the _ssh-keygen_ to generate a public/private authenication key pair, allow users connect withour supplying password, but keys must be generated for each users.

			![ssh-key](images/basic_tool/ssh-key.png)
			> Importing a key to ssh

			![key](images/basic_tool/key.png)
			> my ssh-keygen

5. __`rsync`__

	- `rsync` is a tool for copy, sync data between host and server in Linux
	- **Syntax** `rsync [OPTPIONS] [USER@]HOST:SRC [DEST]`

		* Common [OPTIONS]

			* -r: copy data recursive
			* -a: archive mode
			* -z: pack a data

		![rsync](images/basic_tool/rsync.png)

***

## <div class="a">The End</div>
<style>div.a {text-align:center}</style>

___

<footer> <h3>References</h3>

<a href='http://people.cs.uchicago.edu/~kaharris/cspp51081/Links/unix-resources/linux-fund.pdf' tyle='text-decoration: none'>Overview Linux</a>

<a href='https://linux-training.be/linuxfun.pdf' tyle='text-decoration: none'>Linux Fundamentals</a>
</footer>
