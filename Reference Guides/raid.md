# Linux RAID Config



## setup raid 1 array 
```
mdadm --create --verbose /dev/md0 --level=1 --raid-devices=2 /dev/sdX /dev/sdY
```

## Monitor the status of the raid array
```
cat /proc/mdstat
```

## View details about raid array
```
sudo mdadm --query --detail /dev/md0
```

## Re-Add a drive into an array
```
mdadm /dev/md0 -a /dev/sda
```
or
```
mdadm /dev/md0 -a /dev/sdb
```

## configure smart monitoring

```
sudo smartctl --smart=on --offlineauto=on --saveauto=on /dev/sda
sudo smartctl --smart=on --offlineauto=on --saveauto=on /dev/sdb
```

# bash script to check RAID array is still operational

Save the following file to your home directory.

```bash
#!/bin/bash

userid=$(id -u)
DBUS_SESSION_BUS_ADDRESS="unix:path=/run/user/$userid/bus"
export DBUS_SESSION_BUS_ADDRESS

output=`cat /proc/mdstat | head -n 2 | tail -n 1`

if [ "$output" != "md0 : active raid1 sda[0] sdb[1]" ] && [ "$output" != "md0 :>
then
    /usr/bin/notify-send -a "RAID Check" --urgency=critical "RAID Check Failed">
fi

```

Add execute permissions `chmod 755 raidCheck.sh`.

Schedule the script to run every minute in cron.

```
* * * * *	/home/tim/bin/raidCheck.sh
```