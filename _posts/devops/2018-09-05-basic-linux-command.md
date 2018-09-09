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
| mkdir -m 777 dirname | creates an empty directory with permission |
| chmod -R 777 dirname | make |
| ls | displays the current directory. |


### Explanation

#####Permission

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



