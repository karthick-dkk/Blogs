---
title: "Linux Commands for DevOps"
seoTitle: "linux-commands-for-devops"
datePublished: Sun Aug 11 2024 04:39:40 GMT+0000 (Coordinated Universal Time)
cuid: clzp2sp2l000409mh6xnt7huo
slug: linux-commands-for-devops
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/npxXWgQ33ZQ/upload/b9f5d5e0e0a46bcc21cd42695094c8db.jpeg
tags: cloud, ubuntu, linux, devops, devops-articles

---

Hey Folks, ✌️

Welcome to another one! 😊

Here , we will deep dive into commands is used by **DevOps** engineers for day-to-day activities. Command are most important on when comes to Linux. Its Cloud or On-premises at the end we mostly use Linux based machines. We must know about the commands to run the tasks efficiently.

File System:

```bash
df -hT                               --> Check the files system, partiton status
fdisk -l                             --> Check the device all disk details
tree -a                              --> Check direcotory structure 
du  -sh * | sort -h | tail -n 20     --> Sort the file the Size in current directory
du -a /dir/ | sort -n -r | head -n 20 --> Sort the file the Size inlude directory
cat /etc/fstab                        --> Check the current disk mounts,Partition
mkdir -p /tmp/sub_folder1/sub_folder2 --> Create sub directories
```

Process:

```bash
ps -aux | grep -i nginx            --> Check the nginx process,PID,user,etc
ss -tunlp | grep -i nginx           --> Check the nginx servie is listening
journalctl -f -u nginx              --> Check the service logs for nginx  
lsof  /dev/null                     --> Check Open Files 
lsof -u karthick                    --> Check Open Files for user karthick
lsof -i TCP:80                      --> Check Open Files for port 80 used 
top                                 --> Task Manager ( Process,CPU,Memory )
htop                                --> Advanced Task Manager
free -h                             --> Check RAM info
lscpu                               --> check the CPU info
sync; echo > 3 /proc/sys/vm/drop_caches --> Remove the cache memory
pkill <process>                      --> Kill the process
kill -9 <PID>                        --> Kill the pid of the process
loginctl                             --> Login session details 
logintctl terminate-user <user_name> --> Terminate the user who logged 
```

Service:

```bash
systemctl status nginx        --> Check 'nginx' status 
service nginx status          --> Check 'nginx' status 
sudo systemctl restart nginx  --> Restart 'nginx' status 
ss -tunlp | grep -i nginx     --> Check 'nginx' port
```

Package:

```plaintext
apt install <package>              --> Install the package
apt remvoe <package>               --> Remove the package
apt purge <package>                --> Remove the package also data,config files 
apt autoremove                     --> Remove unused packages
apt update                         --> Update the application packages
apt upgrade                        --> Upgrade the all packages
dpkg -i <package.deb>              --> Install the downloaded package.deb file
```

Misc:

```bash
sudo echo "shutdown -h now" | at -m 00:00 --> Shutdown the machine at 12 AM ( without using Crontab )
atq                        --> List jobs in at
atrm 2                     --> Delete the 2nd task
init 6                     --> Restart the machine
Text Search:
```

Advanced :

```bash
&&  --> Execute when first command sucess, then proceed next command 
Ex: apt update && upgrade
|| --> Execute when first command failed, then proceed next command 
Ex: apt update || apt autoremove
;  --> Execute the command continuosly
Ex: echo 1; echo 3;
```

Text:

```bash
grep karthick log.txt        -->  search "karthick"  in file 
grep -i karthick log.txt     --> search ( Karhick,KARTHICK) without case-sensitive 
grep "text1|value1" log.txt  --> use two values in log
awk '{print $2}' /file       --> Print 2nd column files in all lines 
awk 'NR==1 {print $2}' file    --> Print '1st' row and '2nd' Column only
grep -rin "host_name"        --> search 'host_name' for all files in current directory
diff log1.txt old_log.txt     --> Check diffrence of two files
```

VIM:

```bash
# Command Mode ( Press  " : " for goto command mode )
:$1,%s/abc/xyz/g    --> Replace "abc" vaules into "xyz"
/abc             --> search "abc"  in file
:x                --> Save and Quit
:se nu            --> Set line numbers
# Normal Mode:
yy                --> Copy the full line
p                 --> Paste the copied line
dd                --> Delete the line
# Insert Mode
i - Go to insert mode
R - Replace 
```

Follow for more: ✌️

LinkedIn: [**https://www.linkedin.com/in/karthick-dkk/**](https://www.linkedin.com/in/karthick-dkk/)

Medium: [**https://karthidkk123.medium.com/**](https://karthidkk123.medium.com/)

Github: [**https://github.com/karthick-dkk/**](https://github.com/karthick-dkk/)

Hashnode: [**https://karthick-dk.hashnode.dev/**](https://karthick-dk.hashnode.dev/)

[**Dev.to**](http://dev.to/): [**https://dev.to/karthickdkk**](https://dev.to/karthickdkk)