# Splunk-SSH-log-monitoring 
This project demonstrates how we monitor SSH logs using Splunk to detect any suspicious activity like brute force attak and any unauthorized access.<br>
We Developed interactive dashboard for real-time visualization and analysis of security events.<br>


# Objective
In this project we basically build a dashboard containing SSH log events : 
1. Total SSH Events
2. Successful logins
3. failed logins
4. Connection without Authentication
5. failed login by username
6. Possible Brute force
7. Visualize Brute force attack with geo-location
8. SSH Event Trend over Time
9. SSH login Success Vs Failure
10. Top 20 Targeted Destination IPs

# Tools used :
1. Splunk
2. SSH log file

# Steps 
## 1.*Total SSH Events*<br>
    **Query**: source="ssh_logs_new.json" sourcetype="_json" host="LinuxServer" |stats count As "Total SSH Events"<br>
    **Explanation**: this is used to count total ssh events in ssh log file.<br>
               

![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/d8411607ba79eb01a58045a5c17abbfd381d5f2e/Screenshot%20(161).png)


## 2. *Successful logins*<br>
   **Query**: source="ssh_log_new.json" host="LinuxServer"<br>
              event_type="Successful SSH Logins"<br>
              |stats count by id.orig_h | sort -count<br>
   **Explanation**: firstly we upload data that is "ssh_log_new" json file and then extract data from it then we set host as "Linux Server" and event_type which
   we want.<br>
   stats is command used in splunk for count number of successful logins and group them by id<br>
   sort is used for sorting result in descending order<br>

   
![Successful Login](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/ff979a1589eb4ddb2ef4100119b2611671ab934d/Screenshot%20(115).png)


## 3. *Failed login*<br>
   **Query**: source="ssh_log_new.json" host="LinuxServer"<br>
              event_type="Failed SSH Logins"<br>
              |stats count by id.orig_h | sort -count<br>
   **Explantion**: filter only failed SSH logins from ssh_log_new<br>
   
![Failed Login](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/70f7c4ab79e93049a858760d49f4006f19829641/Screenshot%20(116).png)


## 4. *Connection without Authentication*<br>
   **Query**:source="ssh_log_new.json" host="LinuxServer" soucetype="_json"<br>
             event_type="Multiple Failed Authentication Attempts"<br>
             |stats count by id.orig_h | sort -count<br>
   **Explanation**: This is used to filter only those which have many SSH login failure<br>
                    usually indicate *Brute Force Attack*<br>
   
 ![Multiple Failed Authentication Attempts](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/c60f910e8c06c3308eb5a93d6ddfb028114170b0/Screenshot%20(117).png)
 
 
## 5. *Possible Brute force by ip*<br>
    **Query**:source="ssh_log_new.json" host-="LinuxServer" sourcetype="_json"<br>
              event_type="Multiple Failed Authentication Attempts"|top id.orig_h <br>

              
![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/7b44c5c32b9d0a2d0922de69d16c0e72d8b00219/Screenshot%20(76).png)


## 6.*Failed login by username*<br>
   **Query**: source="ssh_log_new.json" host="LinuxServer" sourcetype="_json" |top username<br>
    top is used to show most frequenctly used username in form of bar chart<br>
     **Explanation**:Finds the most frequently occurring usernames. Counts how many times each username appears<br>
    Sorts in descending order and Calculates percentage. Limits results (default: top 10)<br>

   
![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/3e96a2d2671b085e4288520ff9aeb236a48a511d/Screenshot%20(118).png)


## 7. *Brute Force Attack With geo-location*<br>
    **Query**:source="ssh_log_new.json" host="LinuxServer" sourcetype="_json" <br>
              | iplocation id.orig_h | stats count by Country | where isnotnull(Country)<br>
   **Explanation**:iplocation- this command is used to convert ip address to geographical information add other feilds like country, city and other regions.<br>
   stats count by country help to count login from particular country.<br>
   where isnotnull(Country) is used to remove logs where country is missing.<br>


![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/421b26d2bc73bc56823a9e70c77e1f6e1636121a/Screenshot%20(119).png)


## 8. *SSH Event Type Trend over Time*<br>
    **Explantaion**: source="ssh_logs_new.json" |timechart count by event_type limit=10<br>
   **Explanation**: this command show timeline of success,failure and other events . It is important to detect attack spikes and sudden anomalies<br>


   ![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/779a7d915775d830b09dbce4d066010e7a486751/Screenshot%20(145).png)


## 9. *SSH login Success VS Failure*<br>
    **Query**: source="ssh_log_new.json" |top limit=20 auth success<br>
    **Explanation**: show logins in form of true,false and null and count in percentage<br>

   
   ![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/89f9d237268f6ed1ab07e4d0f75ddaf6652a3068/Screenshot%20(152).png)
   

## 10. *Top 20 targeted Destination IPs*<br>
     **source**="ssh_logs_new.json" <br>
     |stats count AS "Total Attempts" by id.resp_h<br>
     | sort -"Total Attempts" | head 20<br>
    **Explanation**:used to count number of events renamed as Total Attempts and are grouped by id.resp_h (destination ip)


   ![image_alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/8fe5450ab2cb2e500fcd48941af2aec5ab2c508c/Screenshot%20(153).png)

   
   
# Final Dashboard


![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/ac2955fc1c10f532e55d20979f433032eee8ad83/Screenshot%20(84).png)
![image alt](https://github.com/Yashita05420/Splunk-SSH-log-monitoring/blob/a116d56893bcca5d5c5daf6bd4dbf46fff893d02/Screenshot%20(150).png)





