---
layout: post
title: "Basic Linux Command"
comments: true
categories: devops
---

### Basic Linux Command

#### Listing files and directories

|COMMAND | Description |
| ------ | ------ |
| cd - | Returns you to your previous working directory |
| cd ~ | Returns you to your login directory |
| cd | Returns you to your login directory |
| cd $HOME | Returns you to your login directory |
| cd / | Takes you to the entire system's root directory. |
| cd /root | Takes you to the home directory of the root user. You must be the root user to access this directory. |
| cd /home | Takes you to the home directory, where user login directories are usually stored |
| cd .. | Takes you to the directory one level up. |
| cd /dir1/dir2/ | Regardless of which directory you are in, this absolute path takes you directly to dir2, a subdirectory of /dir1/. |
| cd ../../dir2/dir3/ | This relative path takes you up two directories, then to dir2/, and finally into its subdirectory dir3/. |
| pwd | displays the current directory. |
| mkdir dirname | make directory |
| chmod -R 777 dirname | Read, write and execute permission to all user group |
| mkdir -m 777 dirname | creates an empty directory with permission |
| ls | displays the file & directory of the current directory. |
| ls -a | list also files/directories which begin with a dot (hidden) |
| ls -l | long listing format. Displays permissions, user and group, time stamp, size, etc. |
| ls -r | for directories, all sub-directories will be displayed recursively. |
| ls directory | displays the file & directory of the corresponding directory. |



#### File management

|COMMAND | Description |
| ------ | ------ |
| cp file1 file2 | copies files or directories. file1 is copied to file2. if file2 already exists, it is overwritten |
| cp -r dir1 dir2 | recursively with all subdirectories & files |
| mv file1 file2 | Rename or move files |
| mv dir1 dir2 | Rename or move directories |
| rm [-irf] file(s)/directory(ies) | Delete files and/or directories. (-i: delete only after confirmation, -r: directories will be recursively deleted, -f: force) |



##### Permission

![Image](../../../../static/img/chmod777.png)

Different combinations:
- 0 – No permission
- 1 – Execute
- 2 – Write
- 3 – Write and execute
- 4 – Read
- 5 – Read and execute
- 6 – Read and Write
- 7 – Read, write and execute

##### echo command
This command will echo whatever you provide it.
```
echo "test"
test

echo $HOME
/home/rakib
```

##### whoami command
This command reveals the user who is currently logged in.
```
whoami
root
```
##### whatis command
This command gives a one line description about the command. It can be used as a quick reference for any command.
```
whatis date
date (1) - print or set the system date and time
```



