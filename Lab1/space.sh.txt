#!/bin/bash
#default value of threshold
threshold=80
#user can change threshold value at cmd line
if(($#==1))
then
        threshold=$1
fi
echo
echo threshold % is ${threshold}%

#get % utilized of both drives

root_util=$(echo `df / | awk '{print $5}'| grep '[0-9][0-9]'`)
boot_util=$(echo `df /boot | awk '{print $5}' | grep '[0-9][0-9]'`)
#get rid of % sign at end of string
root_util=${root_util:0:2}
boot_util=${boot_util:0:2}
echo utilization of / is ${root_util}%
echo util of /boot is ${boot_util}%

#compare threshold to utilized
if((${root_util}>${threshold}))
then
        mail -s "STORAGE WARNING" root@localhost <<< "/ is above 80% utilization"
        echo root notified of storage status
fi
if((${boot_util}>${threshold}))
then
        mail -s "STORAGE WARNING" root@localhost <<< "/boot is above 80% utilization"
        echo root notified of storage status
fi