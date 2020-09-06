#!/bin/bash

echo CPU AND MEMORY RESOURCES----------------------------
echo
echo CPU Load Average: `uptime | awk '{print $8,$9,$10}'`
echo
echo Free RAM: `free -m | awk 'NR==2{print $4}'`MB
echo
echo
echo NETWORK CONNECTIONS---------------------
echo
echo lo bytes received: `cat /proc/net/dev | awk 'NR==4{print $2}' `            bytes transmitted: `cat /proc/net/dev | awk 'NR==4{print $10}'`
echo
echo enp0s3 Bytes received: `cat /proc/net/dev | awk 'NR==3{print $2}'`                 bytes transmitted: `cat /proc/net/dev | awk 'NR==3{print $10}'`
echo
#source checking internet connection: https://unix.stackexchange.com/questions/190513/shell-scripting-proper-way-to-check-for-internet-connectivity
if ping -q -c 1 -W 1 8.8.8.8 >/dev/null
then
        echo Internet connectivity: Yes
else
        echo Internet connectivity: No
fi
echo
echo
echo ACCOUNT INFORMATION---------------------
echo
echo Total users: `cat /etc/passwd | wc -l`     Active users: `who | wc -l`
echo
echo Shells:
echo
echo /sbin/nologin: `cat /etc/passwd | grep /sbin/nologin | wc -l`
echo
echo /bin/bash: `cat /etc/passwd | grep /bin/bash | wc -l`
echo
echo /bin/false: `cat /etc/passwd | grep /bin/false | wc -l`
echo
echo
echo FILESYSTEM INFORMATION---------------------------
echo
echo Total number of files: `find / -type f | wc -l`
echo
echo Total number of directories: `find / -type d | wc -l`
echo