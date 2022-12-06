# Summary of Operations
## Exposed Services

Nmap scan results for each machine reveal the below services and OS details:
$ nmap 192.168.1.90/24

The ip 192.168.1.110 was also discovered in the scan
This scan identifies the services below as potential points of entry:
- **Target 1:**
  - SSH 
  - HTTP
  - NetBios-ssn
  - MicrosoftDS
  - RPCbind 

<img width="437" alt="Open Ports" src="https://user-images.githubusercontent.com/87619948/205858437-77a4a520-88de-4e51-bbcc-d37e84ea21f6.png">

<img width="624" alt="Open Services" src="https://user-images.githubusercontent.com/87619948/205858447-45233e6b-bfe0-44e8-80f1-c992590817fe.png">

The following vulnerabilities were identified on each target:
- **Target 1**
  - Services discoverable by nmap
  - Ssh open access 
  - wp enumeration scan available for use
  - Weak password policy
  - Privilege escalation via python commands that are open source
  - Use of wordpress increases vulnerabilities and risk of exploitation

- **Target 2**
  - Directory not hidden, available via web access
  - Unrestricted file upload, leading to malicious script uploading and reverse shell convention via netcat
  - Services and open ports discoverable via nmap
  - Use of wordpress increases vulnerabilities and risk of exploitation

<img width="483" alt="Wordpress Exposed" src="https://user-images.githubusercontent.com/87619948/205859379-4cea21a3-f5c4-4867-bf3a-94fecb66cd33.png">

<img width="458" alt="Wordpress Scan" src="https://user-images.githubusercontent.com/87619948/205859389-dac4fd56-9677-4dce-9985-af6e7c580187.png">

## Exploitation
The Red Team was able to penetrate Target 1 and retrieve the following confidential data:

- **Target 1**
  - **flag1.txt:**

<img width="512" alt="target 1 flag 1" src="https://user-images.githubusercontent.com/87619948/205860132-0ed21efc-5eff-42de-8838-975cd544218a.png">

  - Exploit Used
    - Wordpress Enumeration scan
    - wpscan -- url http://192.168.1.110/wordpress -- enumerate u
    - Establishing a reverse shell via netcat allowed for the use of the find command to search for files containing “flag” which output the result of flag1.txt

  - **flag2.txt**
  
  <img width="545" alt="target 1 flag 2" src="https://user-images.githubusercontent.com/87619948/205860908-63e22a2b-6071-4208-9eaa-eb627aad8808.png">
  
 - Exploit Used
   - Wordpress Enumeration scan
   - wpscan -- url http://192.168.1.110/wordpress -- enumerate u
   - Establishing a reverse shell via netcat allowed for the use of the find command to search for files containing “flag” which output the result of flag2.txt

  - flag3.txt and flag4.txt: 

<img width="565" alt="Target 1 flag 3:4" src="https://user-images.githubusercontent.com/87619948/205861497-6c9c8752-8bf9-47ac-b58b-6e6769222605.png">

  - Exploit Used
    - Weak password policy and mysql username/password found in unencrypted file
    - Command: show tables , select * from wp_posts
    - Establishing a reverse shell via netcat allowed for the use of the find command to search for files containing “flag” which output the result of flag1.txt


