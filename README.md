🔐 Endpoint Threat Detection & Security Monitoring Using Wazuh

📌 Project Overview :

This project is a practical cybersecurity lab focused on **endpoint security monitoring and threat detection using Wazuh.
The main purpose of this project is to monitor a Windows endpoint, collect security events, detect suspicious activities, monitor file changes, assess security configurations, review vulnerabilities, investigate alerts, and understand how security events are mapped to the MITRE ATT&CK framework.
In this project, a Wazuh Agent was installed on a Windows endpoint. The Wazuh Manager, Wazuh Indexer, and Wazuh Dashboard were used for collecting, processing, storing, visualizing, and investigating security data.

🎯 Objectives :

The main objectives of this project are:
- Monitor a Windows endpoint using Wazuh
- Collect and analyze Windows security events
- Detect failed login attempts
- Perform File Integrity Monitoring (FIM)
- Detect file creation and modification
- Monitor file integrity and checksum changes
- Perform Security Configuration Assessment (SCA)
- Review endpoint hardware and software information
- Monitor network information, processes, and services
- Understand vulnerability detection
- Analyze Wazuh security rules and alerts
- Map security events to MITRE ATT&CK
- Understand the Active Response mechanism
- Practice basic SOC alert investion

🏗️ Project Architecture :

The project uses the following architecture:

Windows Endpoint  
↓  
Wazuh Agent  
↓  
Wazuh Manager  
↓  
Wazuh Indexer  
↓  
Wazuh Dashboard

1.Windows Endpoint :

The Windows laptop acts as the monitored endpoint.
The Wazuh Agent installed on the endpoint collects security-related information such as:

- Windows Event Logs
- File changes
- System information
- Hardware information
- Installed software
- Running processes
- Windows services

2.Wazuh Agent :

The Wazuh Agent runs on the Windows endpoint.
Its main responsibility is to collect security telemetry and send the collected information to the Wazuh Manager.
The configured agent was:

- Agent Name: LAPTOP
- Agent ID: 001

3.Wazuh Manager :

The Wazuh Manager receives events from the Wazuh Agent.
It analyzes events using Wazuh rules and generates security alerts when matching conditions are detected.

4.Wazuh Indexer :

The Wazuh Indexer stores and indexes security events and alerts.
This allows the collected information to be searched and analyzed.

5.Wazuh Dashboard :

The Wazuh Dashboard provides a graphical interface for monitoring and investigating security information.

It was used to view:

- Security alerts
- Agent information
- FIM events
- SCA results
- Vulnerability information
- IT Hygiene information
- MITRE ATT&CK mappings
- Rule details


 🛠️ Technologies and Tools Used

- Wazuh
- Wazuh Agent
- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Docker
- Windows 11
- PowerShell
- Windows Event Logs
- MITRE ATT&CK
- CIS Security Benchmark


⚙️ Environment Setup :

1. Wazuh Server Environment

Docker was used to run the Wazuh server-side components.
The main Wazuh components were:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

The running containers were verified using:

powershell : docker ps

2. Windows Wazuh Agent
The Wazuh Agent was installed on the Windows endpoint.
The main configuration file is: "C:\Program Files (x86)\ossec-agent\ossec.conf"

The configuration file contains settings for event collection, File Integrity Monitoring, Security Configuration Assessment, and other endpoint monitoring features.
📊 Windows Event Monitoring
Wazuh was configured to collect Windows Event Channels.
The monitored channels included:
Application, Security, System

The Security channel is particularly important for monitoring authentication and other security-related events.
Example configuration:
<localfile>
    <location>Security</location>
    <log_format>eventchannel</log_format>
</localfile>

The Wazuh Agent collects these events and sends them to the Wazuh Manager for analysis.
🔑 Authentication Monitoring :
Windows generates security events for authentication activity.
Two important Windows Security Event IDs are:
4624 → Successful Logon
4625 → Failed Logon

These events can be investigated to understand authentication activity on the endpoint.
🚨 Failed Logon Detection :
During the project, a failed Windows login event was investigated.
The event was:
Event ID: 4625
The event indicated:
An account failed to log on.

The event contained information such as:
- Target username
- Logon type
- Failure reason
- Source address
- Authentication package
- Process information
Example failure reason:
Unknown user name or bad password.

Wazuh collected the Windows event and generated an alert based on the corresponding detection rule.
🔎 Failed Login Investigation Process :
The detection workflow was:
Login Attempt
      ↓
Authentication Failure
      ↓
Windows Event ID 4625
      ↓
Wazuh Agent
      ↓
Wazuh Manager
      ↓
Rule Matching
      ↓
Security Alert
      ↓
Alert Investigation

This demonstrates a basic SOC-style authentication monitoring workflow.
📁 File Integrity Monitoring (FIM) :
What is FIM?
File Integrity Monitoring is used to detect changes to monitored files and directories.
Wazuh FIM can identify activities such as:
- File creation
- File modification
- File deletion
- Permission changes
- Ownership changes
- Attribute changes
- Hash or checksum changes
🧪 FIM Practical Test
A dedicated test directory was configured:
C:\soc-fim-test

The Wazuh Agent log confirmed that the directory was being monitored.
A test file was created and modified inside this directory.
Example:
New-Item C:\soc-fim-test\test.txt

The file was then modified:
Set-Content C:\soc-fim-test\test.txt "Security test"

Wazuh detected the file activity.
🔐 File Integrity and Checksum :
When a monitored file changes, its integrity information can also change.
The basic concept is:
Original File
     ↓
Original Hash
     ↓
File Modified
     ↓
New Hash
     ↓
Hash Difference
     ↓
Wazuh Alert

The project generated an alert:
Integrity checksum changed

The corresponding Wazuh rule was:
Rule ID: 550
Level: 7

This demonstrates practical File Integrity Monitoring.
🛡️ Security Configuration Assessment (SCA) :
What is SCA?
Security Configuration Assessment checks whether a system follows recommended security configuration standards.
In this project, the Windows endpoint was assessed using a CIS Windows security benchmark.
The assessment produced:
- Passed checks
- Failed checks
- Not applicable checks
SCA helps identify configuration weaknesses that may require security improvement.
Important:
SCA failures represent configuration compliance gaps. They do not automatically mean that the endpoint has been compromised.

🖥️ IT Hygiene :
Wazuh provides endpoint inventory information through IT Hygiene.
The following categories were reviewed:
Hardware : Hardware information such as CPU, memory, operating system, and system details.
Software : Installed software and application information.
Network : Network-related endpoint information.
Processes : Running processes on the Windows endpoint.
Services : Windows services running on the endpoint.
IT Hygiene provides visibility into the endpoint and helps analysts understand what is running on a system during security investigations.

🐛 Vulnerability Detection :
Wazuh provides vulnerability detection capabilities that can identify known vulnerabilities associated with installed software.
The basic process is:
Installed Software
       ↓
Software Version
       ↓
Vulnerability Matching
       ↓
Known Vulnerability / CVE
       ↓
Security Analysis

This helps security teams understand potential vulnerabilities present on monitored endpoints.
🎯 MITRE ATT&CK Mapping :
MITRE ATT&CK is a knowledge base that categorizes adversary tactics and techniques.
Wazuh can map certain security alerts to MITRE ATT&CK techniques.
During the FIM investigation, the alert was mapped to:
MITRE ID: T1565.001
Technique: Stored Data Manipulation
Tactic: Impact

The mapping provides additional context for understanding the type of activity associated with an alert.
A MITRE mapping by itself does not prove that a malicious attack occurred. The complete event context must be investigated before determining whether activity is malicious.
📜 Wazuh Rules and Alerts :
Wazuh uses detection rules to analyze incoming security events.
When an event matches a rule, Wazuh can generate an alert.
Example:
Rule ID: 550
Rule Level: 7
Description: Integrity checksum changed

The alert can also contain:
- Event information
- Rule groups
- Agent information
- MITRE ATT&CK mapping
- Compliance information 

🔬 Alert Investigation :
The basic alert investigation process used in this project was:

Security Alert
      ↓
Identify Rule
      ↓
Check Event Details
      ↓
Identify Endpoint
      ↓
Understand Activity
      ↓
Check MITRE Mapping
      ↓
Determine Appropriate Response

This provides practical experience with basic SOC alert investigation.
⚡ Active Response
Wazuh provides an Active Response mechanism that can execute predefined actions based on configured security events.
The Wazuh Active Response log was checked at:
C:\Program Files (x86)\ossec-agent\active-response\active-responses.log

The log showed execution of:
active-response/bin/restart-wazuh.exe

The entry included:
Starting
Command: add
Module: wazuh-execd
Ended

This demonstrated the Active Response execution mechanism in the environment.
🔄 Active Response Workflow
Security Event
      ↓
Wazuh Rule
      ↓
Alert
      ↓
Active Response
      ↓
Configured Action

Active Response can be used to automate predefined defensive actions.
🧠 Threat Detection vs Malware Detection
This project focuses primarily on:
- Endpoint Security Monitoring
- Threat Detection
- File Integrity Monitoring
- Authentication Monitoring
- Security Configuration Assessment
- Vulnerability Monitoring
- Alert Investigation
- MITRE ATT&CK Mapping
- Active Response
No real malware was executed as part of this project.
Therefore, the project is best described as:
Endpoint Threat Detection and Security Monitoring Using Wazuh
rather than simply:
Malware Detection Using Wazuh

🔄 Complete Project Workflow :
Start
  ↓
Prepare Docker Environment
  ↓
Start Wazuh Manager
  ↓
Start Wazuh Indexer
  ↓
Start Wazuh Dashboard
  ↓
Install Wazuh Agent on Windows
  ↓
Connect Agent to Manager
  ↓
Collect Windows Security Events
  ↓
Configure File Integrity Monitoring
  ↓
Generate Test File Activity
  ↓
Detect File Changes
  ↓
Investigate Windows Authentication Events
  ↓
Perform SCA Assessment
  ↓
Review IT Hygiene
  ↓
Review Vulnerability Information
  ↓
Analyze Wazuh Rules and Alerts
  ↓
Review MITRE ATT&CK Mapping
  ↓
Verify Active Response
  ↓
Document Results
  ↓
End

📸 Project Screenshots :
The project screenshots demonstrate the practical implementation and investigation process.
Screenshot 01 - Wazuh Overview
Shows the main Wazuh dashboard and security monitoring environment.
Screenshot 02 - Agent Status
Shows the connected Windows endpoint and Wazuh Agent information.
Screenshot 03 - Failed Logon Detection
Shows detection of a Windows failed authentication event.
Screenshot 04 - Windows Event Investigation
Shows detailed information from the Windows Security event.
Screenshot 05 - File Integrity Monitoring
Shows Wazuh FIM alerts generated from file activity.
Screenshot 06 - Security Configuration Assessment
Shows the CIS-based Windows security configuration assessment.
Screenshot 07 - IT Hygiene Hardware
Shows endpoint hardware information.
Screenshot 08 - IT Hygiene Software
Shows installed software information.
Screenshot 09 - IT Hygiene Network
Shows endpoint network information.
Screenshot 10 - IT Hygiene Processes
Shows running processes on the endpoint.
Screenshot 11 - IT Hygiene Services
Shows Windows services.
Screenshot 12 - Vulnerability Detection
Shows the Wazuh vulnerability monitoring section.
Screenshot 13 - MITRE ATT&CK Mapping
Shows the MITRE ATT&CK technique mapping associated with a security event.
Example:
T1565.001
Stored Data Manipulation

Screenshot 14 - Active Response
Shows Active Response execution information from the Wazuh Agent.
Screenshot 15 - Rule and Alert Analysis
Shows Wazuh rule and alert information.
Example:
Rule ID: 550
Level: 7
Description: Integrity checksum changed

🧠 Key Concepts Learned :
Through this project, I gained practical knowledge of:
- Endpoint security monitoring
- SIEM concepts
- Wazuh architecture
- Wazuh Agent
- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Windows Event Logs
- Authentication monitoring
- Event ID 4624
- Event ID 4625
- File Integrity Monitoring
- File hash and checksum monitoring
- Security Configuration Assessment
- CIS security benchmarks
- Endpoint inventory
- IT Hygiene
- Vulnerability monitoring
- Wazuh rules
- Wazuh alerts
- Alert investigation
- MITRE ATT&CK
- Active Response
- SOC monitoring workflow

📈 Skills Demonstrated
Technical Skills :
- Wazuh
- Windows Security Monitoring
- PowerShell
- Docker
- Windows Event Logs
- File Integrity Monitoring
- Security Configuration Assessment
- Vulnerability Monitoring
- MITRE ATT&CK
- Security Alert Analysis

SOC Skills :
- Security event monitoring
- Alert investigation
- Endpoint monitoring
- Rule analysis
- Event analysis
- Threat detection concepts
- Incident investigation workflow
- Security documentation

🎓 Learning Outcome :
This project provided practical hands-on experience with endpoint security monitoring using Wazuh.
I learned how a security monitoring platform collects endpoint telemetry, analyzes security events, generates alerts, maps events to security frameworks, and provides information that can be used for investigation.
The project helped me understand practical concepts related to:
- Endpoint monitoring
- Authentication monitoring
- File integrity monitoring
- Security configuration assessment
- Vulnerability awareness
- Alert investigation
- MITRE ATT&CK
- Automated response

🏁 Conclusion :
The Endpoint Threat Detection & Security Monitoring Using Wazuh project demonstrates a practical endpoint security monitoring environment.A Windows endpoint was connected to Wazuh and monitored for security events, authentication failures, file changes, configuration issues, endpoint information, and security alerts.The project also demonstrated how Wazuh rules can generate alerts, how alerts can be investigated, and how security events can be associated with MITRE ATT&CK techniques.This project provided practical exposure to concepts used in SOC operations, endpoint security monitoring, threat detection, and security alert investigation.

⚠️ Disclaimer :
This project was created for educational and cybersecurity learning purposes in a controlled lab environment.
No real malware was executed as part of this project.
All testing and monitoring activities were performed on systems and environments controlled for this lab.

👨‍💻 Author :
Shenba Murugan
Computer Science Engineering Graduate | Cybersecurity Learner

Areas of Interest :
- Cybersecurity
- SOC Operations
- Security Monitoring
- Network Security
- Threat Detection
- Incident Response
- Endpoint Security

⭐ Project Highlights :

✔ Wazuh Endpoint Monitoring
✔ Windows Security Event Monitoring
✔ Failed Login Detection
✔ File Integrity Monitoring
✔ Security Configuration Assessment
✔ Endpoint Inventory
✔ Vulnerability Monitoring
✔ MITRE ATT&CK Mapping
✔ Rule & Alert Investigation
✔ Active Response
✔ SOC Monitoring Workflow
