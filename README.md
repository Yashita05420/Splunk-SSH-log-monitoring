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
we go to upload data ![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/a1e7e49bdae6370e2f79220f23b9da516105d075/Screenshot%20(43).png)
![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/a4ceb1e8f88808303c68cff0717d0136ff8a44c0/Screenshot%20(44).png)
![image alt]{https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/1ae46fb897aa4d4e7779196c884174085a16651f/Screenshot%20(46).png)
