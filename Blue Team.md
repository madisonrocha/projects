# Summary of Operations
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
## Network Topology
## Description of Targets
## Monitoring the Targets
## Patterns of Traffic & Behavior
## Suggestions for Going Further
