# Summary of Operations
## Network Topology
The following machines were identified on the network:

- Kali Linux
  - Operating System: Kali Linux
  - Purpose: Used to exploit vulnerable machines, use enumeration scans, set alerts, and review logs. A standard Kali Linux machine for use in penetration testing.
  - IP Address: 192.168.1.90
- Target 1
  - Operating System: Linux 3.2-4.9
  - Purpose: Machine used to be attacked and gather log data from. Exposes a vulnerable WordPress server.
  - IP Address: 192.168.1.110
- Target 2
  - Operating System: Linux 3.2-4.9
  - Purpose: Victim Machine used to be attacked and find flags on.
  - IP Address: 192.168.1.115
- Elk Server
  - Operating System: Linux Ubuntu 18.4.4
  - Purpose: Run kibana to analyze log data (SIM).
  - IP Address: 192.168.1.100
- Capstone
  - Operating System: Linux Ubuntu 18.4.1
  - Purpose: Base VM used to access others via HyperV. Filebeat and Metricbeat are installed and will forward logs to the ELK machine.
  - IP Address: 192.168.1.105

## Description of Targets
Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

- Alert 1: Excessive HTTP Errors
  Alert 1 is implemented as follows:
    -Metric: http.response.status_code (HTTP response code)
    -Threshold: Select the packetbeat indice
    - WHEN count() GROUPED OVER top 5 'http.response.status_code' IS ABOVE 400 FOR THE LAST 5 minutes
    - Vulnerability Mitigated: Brute Force Attacks - the testing of several passwords against one username in attempts to gain credentials to a system    which can allow for unwanted access into a system by people who are not supposed to have access to a system, violating confidentiality and integrity of the CIA triad.  
    - Reliability: Highly Reliable. Anytime the response status codes are above the threshold of 400 the alert is triggered which. If the alert is set according to the average amount of traffic on a given website, anything above that threshold is most likely malicious and therefore action should be taken. 
![Excessive HTTP Errors](https://user-images.githubusercontent.com/87619948/205848923-d5075b8b-1375-47f5-bd9f-60eaa57cf4bd.PNG)

## Monitoring the Targets
## Patterns of Traffic & Behavior
## Suggestions for Going Further

