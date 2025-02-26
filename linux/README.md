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
## cat
  display file content
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
## grep <string>
  grep [options] pattern <source>
  (grep "error" /var/log/syslog)
  search for specific patterns within files.
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
## wc
  wc [options] [file...]
  (wc myfile.txt)
  count the number of lines, words, characters, and bytes in a text file or input provided.

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
##

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
