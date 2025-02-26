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
## chmod
  chmod [options] mode file
  (chmod 755 myfile.txt) - Set permissions using numeric mode.
  (chmod u+x myfile.txt) - Set permissions using symbolic mode
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


  
