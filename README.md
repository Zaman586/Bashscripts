Step 1: Create the Bash Script

    Create the script file, for example, system_info_logger.sh:

bash

nano ~/system_info_logger.sh

    Add the following content to system_info_logger.sh:

bash

#!/bin/bash
# Script to log system information along with the current date and time

# Define the log file
LOG_FILE=~/timestamp_system_info.log

# Get the current date and time
CURRENT_TIME=$(date '+%Y-%m-%d %H:%M:%S')

# Get CPU information
CPU_INFO=$(lscpu | grep 'Model name:')
# Alternatively, to get CPU load average:
# CPU_LOAD=$(uptime)

# Get RAM information
RAM_INFO=$(free -h | grep 'Mem:')
# Alternatively, to get detailed RAM usage:
# RAM_DETAIL=$(free -h)

# Get root filesystem usage
ROOT_USAGE=$(df -h / | grep '/dev/')

# Append the timestamp and system information to the log file
echo "Timestamp: $CURRENT_TIME" >> $LOG_FILE
echo "CPU Info: $CPU_INFO" >> $LOG_FILE
echo "RAM Info: $RAM_INFO" >> $LOG_FILE
echo "Root Filesystem Usage: $ROOT_USAGE" >> $LOG_FILE
echo "------------------------------------------------" >> $LOG_FILE

    Save and close the file (Ctrl + X, then Y, then Enter).

    Make the script executable:

bash

chmod +x ~/system_info_logger.sh

Step 2: Set Up the Cron Job

    Open the crontab file for editing:

bash

crontab -e

    Add the following line to the crontab file to run the script every 5 minutes (adjust the timing as needed):

bash

*/5 * * * * ~/system_info_logger.sh

This line tells cron to execute ~/system_info_logger.sh every 5 minutes. Adjust the timing (*/5 * * * * means every 5 minutes) to suit your requirements.

    Save and close the crontab file. If using nano, press Ctrl + X, then Y, then Enter.

Step 3: Verify the Cron Job

To verify that the cron job is set up correctly, you can list the cron jobs for your user:

bash

crontab -l

You should see the entry:

bash

*/5 * * * * ~/system_info_logger.sh

Step 4: Check the Script Execution

After a few minutes, check the timestamp_system_info.log file to see if it is logging the system information as expected:

bash

cat ~/timestamp_system_info.log
