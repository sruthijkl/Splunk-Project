Splunk Cybersecurity Mini SIEM Project Summary
Project Overview:

I built a simple Security Information and Event Management (SIEM) system using Splunk to monitor Linux authentication logs (auth.log) and detect failed SSH login attempts. This helps me identify possible brute force attacks on my system.



Data Used:

I used a sample Linux authentication log file containing 3 failed login events:


Aug 10 10:33:21 ubuntu sshd[1024]: Failed password for invalid user root from 192.168.1.101 port 2234 ssh2  
Aug 10 10:34:05 ubuntu sshd[1025]: Failed password for invalid user admin from 192.168.1.102 port 2235 ssh2  
Aug 10 10:35:47 ubuntu sshd[1026]: Failed password for invalid user test from 192.168.1.103 port 2236 ssh2  




Key Actions:

1. Data Ingestion:
   I uploaded this auth.log file into Splunk so I could index and analyze it.

2. Search & Extraction:
   I wrote a Splunk search query to find all events containing "Failed password" and used regex to extract the source IP addresses:

spl
index=* "Failed password"
| rex "from\s+(?<src>\d{1,3}(?:\.\d{1,3}){3})"
| stats count by src
| sort -count
| head 20


3. Dashboard Creation:
   I created a dashboard panel (a bar chart) in Splunk to visualize the top 20 IP addresses responsible for failed login attempts, giving me a clear view of suspicious activity.



 Outcome:

I successfully identified failed SSH login attempts from three unique IP addresses in my sample logs. The dashboard provides an easy way to monitor this activity visually and helps me keep track of potential brute force attacks.
Future Thoughts:

Simulate larger datasets or repeated attacks for more detailed analysis.
Set up alerts to notify me when an IP exceeds a certain number of failed login attempts.
Add geo-location enrichment and build additional dashboards for better insights.
