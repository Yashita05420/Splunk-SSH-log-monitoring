# Splunk-SSH-log-monitoring 
This project demonstrates how we monitor SSH logs using Splunk to detect any suspicious activity like brute force attak and any unauthorized access. We Developed interactive dashboard for real-time visualization and analysis of security events.
## Objective
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
1. We detect successful logins :
   Query: source="ssh_log_new" host="LinuxServer"
   event_type="Successful SSH Logins"
   |stats count by id.orig_h | sort -count
   Explanation: firstly we upload data that is "ssh_log_new" json file and then extract data from it then we set host as "Linux Server" and event_type which
   we want.
   stats is command used in splunk for count number of successful logins and group them by id
   sort is used for sorting result in descending order

   
![Successful Login](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/ff979a1589eb4ddb2ef4100119b2611671ab934d/Screenshot%20(115).png)


3. Detect Failed logins:
   Query: source="ssh_log_new" host="LinuxServer"
          event_type="Failed SSH Logins"
          |stats count by id.orig_h | sort -count

   
![Failed Login](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/70f7c4ab79e93049a858760d49f4006f19829641/Screenshot%20(116).png)


5. source="ssh_log_new" host="LinuxServer" soucetype="json"
          event_type="Multiple Failed Authentication Attempts"
          |stats count by id.orig_h | sort -count

   
 ![Multiple Failed Authentication Attempts](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/c60f910e8c06c3308eb5a93d6ddfb028114170b0/Screenshot%20(117).png)

 
![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/7b44c5c32b9d0a2d0922de69d16c0e72d8b00219/Screenshot%20(76).png)


6. source="ssh_log_new" host="LinuxServer" sourcetype="json" |top username
   top is used to show most frequenctly used username in form of bar chart

   
![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/3e96a2d2671b085e4288520ff9aeb236a48a511d/Screenshot%20(118).png)


7. source="ssh_log_new" host="LinuxServer" sourcetype="json" | iplocation id.orig_h | stats count by Country | where isnotnull(Country)
   iplocation- this command is used to convert ip address to geographical information add other feilds like country, city and other regions.
   stats count by country help to count login from particular country.
   where isnotnull(Country) is used to remove logs where country is missing.


![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/421b26d2bc73bc56823a9e70c77e1f6e1636121a/Screenshot%20(119).png)


8. source="ssh_logs_new.json" |timechart count by event_type limit=10
    this command show timeline of success,failure and other events . It is important to detect attack spikes and sudden anomalies

   ![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/779a7d915775d830b09dbce4d066010e7a486751/Screenshot%20(145).png)


9. source="ssh_logs_new.json" |stats count AS "Total Attempts" by id.resp_h | sort -"Total Attempts" | head 20
    used to count number of events renamed as Total Attempts and are grouped by id.resp_h (destination ip)
   ![image_alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/8fe5450ab2cb2e500fcd48941af2aec5ab2c508c/Screenshot%20(153).png)

   
   
## Final Dashboard


![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/ac2955fc1c10f532e55d20979f433032eee8ad83/Screenshot%20(84).png)
![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/a116d56893bcca5d5c5daf6bd4dbf46fff893d02/Screenshot%20(150).png)





