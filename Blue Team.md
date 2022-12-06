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
The target of this attack was: Target 1 (192.168.1.110).
Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

## Monitoring the Targets
Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

- **Alert 1: Excessive HTTP Errors**
  Alert 1 is implemented as follows:
   - **Metric:** http.response.status_code (HTTP response code)
   - **Threshold:** Select the packetbeat indice
   - WHEN count() GROUPED OVER top 5 'http.response.status_code' IS ABOVE 400 FOR THE LAST 5 minutes
   -  **Vulnerability Mitigated:** Brute Force Attacks - the testing of several passwords against one username in attempts to gain credentials to a system which can allow for unwanted access into a system by people who are not supposed to have access to a system, violating confidentiality and integrity of the CIA triad.  
   - **Reliability:** Highly Reliable. Anytime the response status codes are above the threshold of 400 the alert is triggered which. If the alert is set according to the average amount of traffic on a given website, anything above that threshold is most likely malicious and therefore action should be taken. 
 
![Excessive HTTP Errors](https://user-images.githubusercontent.com/87619948/205848923-d5075b8b-1375-47f5-bd9f-60eaa57cf4bd.PNG)

- **Alert 2: HTTP Request Size Monitor**
  Alert 2 is implemented as follows:
  
   -  **Metric:** http.request.bytes (HTTP request in bytes)
   -  **Threshold:** Select the packetbeat indice
   - WHEN sum() of http.request.bytes OVER all documents IS ABOVE 3500 FOR THE LAST 1 minute
   - **Vulnerability Mitigated:** Buffer Overflow, which can cause servers to go down if they cannot handle the size of the http request body, and cause memory leaks, and the leaking of inodes, which can lead to sensitive information being exposed, because it cannot intake all of it the new data and get rid of the old data at the same time in a proper manner. 
   - **Reliability:** This monitor is highly reliable. HTTP request sizes are fairly stable and predictable, therefore anything that differs would be marked as suspicious and flagged for additional monitoring and/or looking into. 

![Http Request Size Monitor](https://user-images.githubusercontent.com/87619948/205849865-f7eb4466-9562-4c27-91f3-4e2d96ec1ce6.PNG)

- **Alert 3: CPU Usage Monitor**
  Alert 3 is implemented as follows:
   - **Metric:** system.process.cpu.total.pct (single process cpu usage percent)
   - **Threshold:** Select the metricbeat indice
   - WHEN max() OF system.process.cpu.total.pct OVER all documents IS ABOVE 0.5 FOR THE LAST 5 minutes
   - **Vulnerability Mitigated:** DDoS attacks, Cryptojacking - both of these attacks take a high amount of CPU usage to execute, DDoS attacks having the potential to make data from a service unavailable to its users, and cryptojacking having a way to use a users computer power without consent to mine for cryptocurrency.
   - **Reliability:** Medium Reliability. There is no way to predict how much power any given application on a server might need at a given time. Thresholds can be set according to averages, but an alert doesn’t necessarily mean malicious activity as there may be a lot going on at a given time for a particular application that causes it to use more CPU. 

![CPU Usage Monitor](https://user-images.githubusercontent.com/87619948/205850526-962c4acc-7f24-481c-89f9-aa76b8bae144.PNG)

## Suggestions for Going Further
The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:

- **Excessive CPU Usage**
 - **Patch:** Monitoring and alerts 
 - **Why It Works:** By monitoring the use of CPU, as well as setting alerts for any programs taking up an unusual amount of CPU will allow for further inspection of why this is happening. From there it can be determined if the excessive CPU usage is warranted by a specific program, or if it is a malicious threat to a system.

- **Brute Force**
 - **Patch:** strong passwords, account logouts after x amount of failed attempts 
 - **Why It Works:** The use of strong passwords that have the characteristics of complexity, randomness, and length will help mitigate the use of dictionary attacks, as common passwords are usually easy to guess using programs such as john, hydra, or the use of rainbow tables. Locking out accounts after a predetermined amount of failed login attempts will prevent the attacker from being able to continue to try different passwords on a system, as well as alert the account user that someone is trying to gain unauthorized access to an attack.

- **DDoS Attacks**
 - **Patch:** load balancers, server redundancy 
 - **Why It Works:** Using load balancers helps servers to properly handle all of the data that they are receiving without becoming overwhelmed. This can prevent the use of exploits such as buffer overflow, which can cause the leaking of sensitive information. Server redundancy allows for servers to have information readily available on multiple servers, thus if one goes down or is a victim of a DDoS attack, the information is still readily available via another server.  




