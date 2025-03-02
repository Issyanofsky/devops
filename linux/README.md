<div align="center">

# **Linux**

</div>

## pwd
  show present folder location.
## cd
  cange directory.
## clear
  clear screen.
## ls
  list folder.
  ls -alh
## man 
  man <command
  show manual of the command

## mkdir
  mkdir <Folder-Name>
  create new folder
## mv
  mv <fileName> <dest-File_Name>
  move file.
## cp
  cp <fileName> <dest-File_Name>
  copy file.
## rm 
  rm <File_Name>
  delete file
## rmdir
  rmdir <directory_name>
  delete directory (only if its empty)
## rm -rf
  rm -rf <folder-Name>
  delete folder with its all content (including sub dir)
## which
  which <command>
  location of the executable file that would be run when you type a command in the shell.
## whereis
  whereis <command>
  like which but give more detailes (like manunal)
## locate
  locate <file_name>
  find files by name 

  if not exist:
    sudo apt install mlocate
    sudo updatedb
## find
  search for files and directories in a directory hierarchy based on various search criteria such as name, type, size, permissions, and more
  find <directory> -name <filename>
## echo
  echo [string]
  print text or variables
## less
  less <file_name>
  display the contents of a file one screen at a time.
## head
  head <file_name>
  display 10 first lines of a the file.
## tail
  tail <file_name>
  display last 10 lines of a the file.

## |
  command1 | command2
  (ls | grep "file")
  piping - pipe output of one command to the next
## history
  history
  display a list of previously executed commands in the current shell session.
  ### !
  execute the command from history
  !<number-command in history>
## kill programs
  kill <pid> - terminate processes. 
  killall <pid> - Terminate all processes 
  (killall -u username) - Terminate all processes for a user
## pkill
  pkill <process_name>
  (pkill firefox)
  kill a process by name.
## ping
  ping <ip-address>
  pinging to a specific address (check connectivity).
## netstat

  netstat [OPTIONS]
  
  (netstat -l) - Displays only the listening ports.
  
  (netstat -p) - Displays the PID (Process ID).
  
  (netstat -a) - Displays all connections and listening ports.
  
  (network statistics) display information about network connections, routing tables, interface statistics, and other network-related data.
  
## nmap
  nmap [options] [target]
  (nmap -sn 192.168.1.0/24) -Discover hosts on a network without port scanning.
  (Network Mapper) network discovery and security auditing
## wget
  wget [options] <URL>
  (wget https://example.com/file.txt)
  (wget -P /path/to/destination https://example.com/file.txt) - download a file to a specific location.
  download files from the web.
## df
  df - Display disk space for all filesystems
  df -h - Display disk space in human-readable format.
## mount
  sudo mount <folder_name> <destination_folder>
  (mount /dev/sdb1 /mnt/usb)
  mount a filesystem to a specified directory.
## file
  file [options] <file>
  (file example.txt)
  determine the type of a file based on its content and not just its file extension.
## lsblk 
  lsblk [options]
  (lsblk -f) - List block devices with detailed information.
   list information about block devices.
## lscpu
  lscpu
  display detailed information about the CPU architecture.
## free
  free [options]
  display system memory usage.
## swapon
  swapon [options] [device]
  enable swap devices and swap files.
## uptime
  uptime
  display the system's uptime.

## lsmod
  lsmod
  list all currently loaded kernel modules.
## strace
  strace [options] command [arguments...]
  (strace -p <PID>) - trace a process by its PID (Process ID)
  trace system calls and signals made by a program during its execution. 
## ltrace
  ltrace [options] command [arguments...]
  (ltrace ls)
  similar to strace, but it specifically traces library calls (function calls made to shared libraries) instead of system calls.

# text-processing

## tee

  tee - Reads from standard input and writes to both standard output and files simultaneously.

## cut 

  cut - desplay content.

  (cut text.txt)

## sed

  sed - modify, delete, insert, or substitute text within files or output.

  (sed 's/old_text/new_text/' file.txt) - replaces the first occurrence of "old_text" with "new_text" in each line of file.txt.

## paste

  paste - Merges lines of files side by side, combining them into a single line.

  (paste -s <file_name1> <file_name2> - merge those files.

## join

  join - Combines lines of two files based on a common field or column.

## split

  split - Divides a file into smaller chunks based on specified criteria (e.g., line count).

## sort

  sort - Arranges the lines of input data in a specified order (alphabetical, numerical, etc.).
  
  (sort -r <text>) - reverse the list.

## tr

  tr - Translates or deletes characters in a stream of text.

## uniq

  uniq - Filters out repeated lines from input, leaving only unique entries.

## wc

  wc [options] [file...]
  
  (wc myfile.txt)
  
  count the number of lines, words, characters, and bytes in a text file or input provided.

## nl

  nl - umber the lines of a file and then display them, making it easy to see the line numbers.

  (nl file.txt) - display the contents of file.txt with line numbers added at the beginning of each line.

  (nl -b a file.txt) - Numbering only non-empty lines.

## grep

  grep [options] pattern <source> - search for specific patterns (using regular expressions) within files or input streams. 

  (grep 'pattern' file.txt) - Search for a word in a file

  (grep "error" /var/log/syslog)

## strings

  strings <file_Name> - extract printable strings (sequences of printable characters) from binary files, executables, or other non-text files. 

  (strings example.bin) - view the hex dump of a binary file (like an executable, image, or any file).

  (xxd -r -p example.hex > example_reconstructed.bin) - Reverse Operation (Hex to Binary).

## xxd

  xxd - create a hex dump (a representation of binary data in hexadecimal format) of a file or data. It is also capable of converting a hex dump back into binary data, making it a useful tool for analyzing and manipulating binary files.

  xxd [options] [file]

  (xxd example.bin) 
  
  
# locations

## /etc/passwd 

  list of users
  
## /etc/default/useradd 

  tasks for adding user.
  
## /etc/group

  group on the computer
  
## /usr/share/zoneinfo

  time zone setting
  
## /proc
  
  contains a wealth of real-time information about the system's hardware, running processes, kernel parameters, and more.
  
## /var/log

  contain system logs

# Enviroment variable

## env

  display or set environment variables.
  
## export

  export VARIABLE_NAME=value

  (export MY_VAR="Hello, world!")
  
  set environment variables for the current session or for child processes of the current shell.
  
## unset
  
  unset VARIABLE_NAME
  
  (unset MY_VAR)
  
  remove environment variables or shell functions.
  
## Builtin Varibales

  $PATH - list of  executable files.
  
  $HOME - path to the current user's home directory.
  
  $USER - the name of the user logged into the system.
  
  $SHELL - tells you which shell is being used in your terminal.
  
  $PWD - current working directory. This is the directory in which the user is currently operating in the terminal.

# services

## systemctl

  systemctl [OPTION] COMMAND [SERVICE]
  
  used for start, stop, restart, enable, disable, and check the status of services, as well as manage system shutdowns and reboots.
  
  sudo systemctl start <service_name>
  
  (sudo systemctl start nginx)
  
  (sudo systemctl stop nginx)
  
  (sudo systemctl restart nginx)
  
  (systemctl status nginx)
  
  (sudo systemctl enable nginx)
  
  (sudo systemctl disable nginx)

  (systemctl list-unit --type service) - display all services.

# Firewall

  firewall settings in Linux systems that use firewalld (a dynamic firewall manager). 
  
  firewall-cmd [options] [command] [arguments]
  
  (firewall-cmd --state) - Show the current state of the firewall.
  
  (firewall-cmd --reload) - Reload the firewall to apply permanent changes.
  
  (firewall-cmd --add-service=http --permanent) - Allow HTTP service permanently.
  
  (firewall-cmd --get-service) - display service list.
  
  firewall-cmd --add-port=<portNumber/protocol - (firewall-cmd --add-port=80/tcp).

  systemctl restart firewalld - restart firewall

# processes

## ps
  
  ps [options]
  
  display prossess.
  
  (ps -e) - Show all processes running on the system (including those from other users).
  
  (ps -f) - Display full-format listing with additional details (including the parent process ID).
  
  (ps -u <userName>) - Show processes for a specific user.
  
  (ps aux --sort=%cpu) - Sort processes by CPU usage.
  
## jobs
  
  jobs [options]
  
  (jobs -l) - List jobs with more details
  
  list the jobs that are running in the current terminal session.

  ## & 

  some_command &
  
  Start a job in the background:

  ## fg
    
    fg %<jod id> 
    
    Bring a job to the foreground


  ## bg
    
    bg %<jod id> 
    
    Bring a job to the backeground

## nohup

  nohup command [arguments] &

  (nohup ./my_script.sh &)

  No Hang Up. run a command or process in the background, and it ensures that the process will continue running even if the user logs out or the terminal is closed.  

## top

  top

  real-time monitoring tool used to display information about the system’s resource usage, including CPU, memory, and running processes.

# user/group

## USER

    /etc/passwd - user info
  
    /etc/shadow - passwd info

    /etc/group - group info

    #UID

    #USER

    #GID
  
## whoami

    whoami - current logged-in user's username.

## id

  id [OPTION] [USER] - display the user and group information

  id

## su

  su -c <command> <user> - execute command with other user.

  sudo su - - switch to root user.

## useradd

  useradd <user_Name> - create a new user.

  userdell <user_Name> - delete user. 

## passwd

  sudo passwd <user_Name> - Setting or Changing the Password for a User.

## groupadd

  sudo groupadd GROUP_NAME - create a new group.
  
## gpasswd

  gpasswd [OPTION] GROUP_NAME - group password.

  sudo gpasswd -A user GROUP_NAME - Add group administrators.
  
## usermod

  sudo usermod [OPTIONS] USERNAME - modify user accounts.

  (sudo usermod -aG group_name username) - Change a User's Group.

## chmod

  chmod [options] mode file.
  
  (chmod 755 myfile.txt) - Set permissions using numeric mode.
  
  (chmod u+x myfile.txt) - Set permissions using symbolic mode.

## chown

  sudo chown [OPTIONS] OWNER[:GROUP] FILE - change the ownership of files and directories.

  (sudo chown john file.txt) - Change the owner of a file or directory.

  (sudo chown john:admins file.txt) - Change both the owner and the group of a file.

## chgrp

  sudo chgrp GROUP FILE - change the group ownership of a file or directory.

  (sudo chgrp developers file.txt) - Change the group of a file.

  (sudo chgrp -R developers /path/to/directory) - Change the group of a directory recursively (change the group of a directory and all files/subdirectories inside it). 

## umask

  umask [OPTION] [MASK] - set default file permissions to files and directories.

    (umask) - Display the current umask settings.

    (umask 022) - value 022 removes write permissions for group and others.

## sticky bit

  only the file's owner, the directory's owner, and the root user can delete or rename the files inside that directory, regardless of the directory's permissions. 

  (chmod +t directory_name) -  set the sticky bit on a directory.

# Package Management

## gzip

  gzip <file_Name> - compress files and reduce their size.

  (gzip -d filename.gz) - decompress the file.
  (gunzip filename.gz)  - decompress the file (same a gzip -d).

## tar

  tar - combining multiple files or directories into a single archive file. 

  tar -cf <archive.tar> file1 file2 directory/ - archive from one or more files or directories.

## file

  file <file_Name> - return file type.

## dpkg

  dpkg - base tool for managing Debian package (Ubuntu).

    dpkg -i <package.deb> - install package.

    dpkg -r <package.deb> - Remove package.

    dpkg -l <package.deb> - List package.    

## rpm

  rpm - base tool for managing Red Hat package.

    rpm -i <package.rpm> - install package.

    rpm -r <package.rpm> - Remove package.

    rpm -qa <package.rpm> - List package.    


    red-hat | Debian |
    yum     | apt    | update - update.
    yum     | apt    | install <package_name> - install package.
    yum     | apt    | remove <package_name> - remove package.
    yum     | apt    | show - list packages.

# BOOT processes

## Boot processes:
  
  - BIOS - firmware that is built into a computer's motherboard. It is a low-level software responsible for initializing and testing hardware components during the booting process, and it provides an interface between the operating system and the hardware.
  - Bootloader - load the Kernel to memory and start it.
  - kernel - intermediary between the hardware and the software, managing system resources such as the CPU, memory, disk space, and peripheral devices. It essentially controls how the software and hardware communicate.
  - Init - the first process that runs when a Unix-like operating system (like Linux or macOS) boots up. It is the ancestor of all other processes, and its primary responsibility is to initialize the system by starting other essential system services and processes required for the system to function properly.

## SysVinit (Traditional init)

Runlevels: SysVinit uses runlevels (0-6) to define different states of the system:

 - 0: Halt
 - 1: Single-user mode (for maintenance)
 - 2: Multi-user mode (without network)
 - 3: Multi-user mode with network
 - 4: Unused or custom
 - 5: Multi-user mode with graphical interface
 - 6: Reboot

   (init 3) - Switch to runlevel 3 (multi-user mode with network).

## upstart

  (until version 15.04, when it was replaced by systemd).

## systemd

  systemd -  modern init system and service manager used by many Linux distributions. 
  Commands for Managing Services with systemd

    sudo systemctl start <service_name>
    sudo systemctl stop <service_name>
    sudo systemctl restart <service_name>
    sudo systemctl status <service_name>
    sudo systemctl list-units --type=service

## top

  top -  desplay real-time information about the system’s processes, CPU usage, memory usage, and other performance-related statistics.

## lsof 

  lsof  - (List Open Files) command in Linux and Unix-like operating systems is a utility used to display information about files that are currently open by processes.

## Processes 

  Processes - A process is an independent program that is running in its own memory space. 
  
## process thread

  thread - A thread is the smallest unit of execution within a process (like sub process). 
  
## ps

  ps - (process status) command in Linux and Unix-like operating systems is used to display information about the currently running processes.

  (ps -u $USER) - show Processes for the Current User.
  
  (ps -ejH) - show Processes and Their Tree Hierarchy.
  
  (ps -ef) - show Processes in Full Format.
  
  (ps -p <PID>) - find more details about that process.
  
  (ps aux --sort=-%cpu) - find the processes using the most CPU, you can sort by CPU usage.


  
