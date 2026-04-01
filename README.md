# Splunk-SSH-log-monitoring
Splunk Dashboard for SSH logs monitoring
## objective
In this project we basically build a dashboard containing SSH log events : 
1. Successful logins
2. failed logins
3. Connection without Authentication
4. failed login by user
5. Possible Brute force
6. Visualize Brute force attack with geo-location

## Tools used :
1. Splunk
2. SSH log file

## Steps 
### Step 1 : 
We install splunk as splunk is SEIM tool used to analyze , collect and search logs using SPL (Search Processing Language)
now we go to Settings and upload file from which we analyze logs that is **ssh_logs_new.json** file for our dashboard
