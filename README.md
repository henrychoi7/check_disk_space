# check_disk_usage

Shell Script to Monitor Disk Space and Send Alert
By RahulJanuary 8, 20234 Mins Read
It is essential to monitor the disk space on a Linux server to ensure enough free space is available for new files and applications. If the disk becomes full, it can cause issues such as system crashes, data loss, and other problems. To prevent these issues, you can use a shell script to monitor the disk space and send an alert when the available space falls below a certain threshold.

In this article, we will walk through the process of creating a shell script that monitors the disk space and sends an alert when the available space falls below a certain threshold. We will use the df command to check the available disk space and the mail command to send the alert. The features of this script are:

This script can check available free space for multiple disks
You can enable to send an email notification
You can set the threshold values for Warning and Critical conditions
Accept inputs as command line parameters
Step 1: Shell Script to Check Disk Space
I have written this shell script that is capable of checking for the available free space on given disks and notifying the admin if the disk space is low. This script required a Bash shell to run. First copy the shell script on your Linux system. In the next steps, I will provide instructions on how to execute it.

Download this script from GitHub:
https://github.com/tecrahul/shell-scripts/blob/master/check-disk-space/check_disk_space.sh
Otherwise copy the below shell script and paste it to a file on your server.

Step 2: Script Commadn Line Arguments
You can execute the above script manually or using the system crontab. This script required arguments, that can be passed as command line arguments.

Critical Threshold: Set this parameter to send a critical email alert if the free space (%) is less than this. Use -c command line option to provide custom value. The default value is “10”, if not provided.
Warning Threshold: Set this parameter to send a warning email alert if the free space (%) is less than this but more that the critical value. Use -w command line option to provide custom value. The default value is “20”, if not provided.
Disks to Check: Use -d command line option to provide volume name or mount point to check for free space. You can provide multiple disks by providing them multiple times.

Step 2: Execute Script Manually
You can run this script manually or automate it using the system’s crontab. Here are a few examples of how to run this script:

Run this script without any arguments.
bash check_disk_space.sh 
This is similar to:

bash check_disk_space.sh -c 10 -w 20 -d / 
Next, you can change the warning and critical alert levels as per your requirements. For example, send a warning notification if the free space is less than 30% and send a critical notification if the free space is less than 15%.
bash check_disk_space.sh -c 15 -w 30 -d / 
You can also use the device name instead of the mount point.
bash check_disk_space.sh -c 15 -w 30 -d /dev/sda1 
This script also allows the monitoring of multiple disks.
bash check_disk_space.sh -c 15 -w 30 -d / -d /mnt -d /dev/sda1 
Step 4: Adjust Variables in the Script
You can adjust a few variables in the script to customize the environment.

Set the below option to “1”, to send email notifications.
ENABLE_EMAIL_ALERT=1
If the email notification is enabled, Set your email address for sending the notification
NOTIFICATION_EMAIL="youremail@example.com"
Overwrite the default hostname, that will be added in notifications. The default value is the hostname of the system.
HOSTNAME="web-server1"	
Step 4: Schedule Script with Crontab
You can also schedule this script using the system’s crontab to automate. Edit the crontab:

crontab -e 
Add the below crontab entry to run this script hourly.

## Monitor disk space
0   *   *   *   *   bash check_disk_space.sh -w 30 -c 15  -d /

## Monitor disk space (For Mareel and Gambit)
0 * * * * bash check_disk_space.sh -c 15 -w 25 -d /dev/sda1

Save the cron file and close it.

Conclusion
In this tutorial, we have provided a bash script that will check for free disk space and send an email notification to the system administrator. This script can monitor multiple disks at a time. Also, you can set custom thresholds for the warning and critical levels.

https://tecadmin.net/shell-script-to-check-disk-space-and-send-alert/
