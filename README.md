# Sample Work and Projects
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Diagrams/ELKSTACK_DIAGRAM.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the filebeat-playbook.yml file may be used to install only certain pieces of it, such as Filebeat.

  (Ansible/filebeat-playbook.yml)

This document contains the following details:
- Description of the Topologue
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be available, in addition to restricting access to the network.

The jumpbox was purposed as the gateway access point into the web server machines which allowed access through a key generated for ssh usage. Adding the load balancer allowed for stability accross the web servers. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.

Filebeat looks for and processes log data according to the parameters given and forwards all of the changes into Elasticsearch. 
Metricbeat records system resource usage and forwards the metrics into ELasticsearch for further analyzation.

The configuration details of each machine may be found below.


| Name     | Function   | IP Address | Operating System |
|----------|------------|------------|------------------|
| Jump Box | Gateway    | 10.0.0.5   | Linux            |
| Web-1    | Web Server | 10.0.0.6   | Linux            |
| Web-2    | Web Server | 10.0.0.8   | Linux            |
| Web-3    | Web Server | 10.0.0.10  | Linux            |
| Elk      | Elk Stack  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Machines within the network can only be accessed by the jumpbox.


A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible  | Allowed IP Addresses |
|----------|----------------------|----------------------|
| Jump Box | Yes  Port 22         | personal private ip  |
| Web-1,2,3| No                   | Web LB 20.69.121.107 |
| Web LB   | Yes  Port 80         |                      |
| Elk      | Yes  Port 5601, 9200 | 10.0.0.0/16          |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it helps with the representation of Infrastructure as Code (IAC) making management of servers esier, and reduces errors in configuration.

The playbook implements the following tasks:
- Install Docker: downlaods and install the docker code to the server download image; etc._
- Install Python3: TODO
- Install Docker Module: TODO
- Download/Launch Elk: TODO

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.6
- 10.0.08
- 10.0.0.10
- 10.1.0.4

We have installed the following Beats on these machines:
- Filebeat and Metricbeat were installed on Web-1, Web-2, and Web-3

These Beats allow us to collect the following information from each machine:
- Filebeats allowed us to monitor system login activity and metricbeats is used to monitor resource usage across the platform.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the hosts file to include elk and the destination use
- Run the playbook, and navigate to kibana to check that the installation worked as expected.


