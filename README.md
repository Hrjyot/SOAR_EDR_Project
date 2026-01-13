# SOAR_EDR_Project
SOAR + EDR Automation: LimaCharlie detection rules trigger Tines workflows for Slack alerts, analyst approval, and instant endpoint isolation. Features LaZagne credential dumper testing on Windows 11 VM. Live demo of detection-to-response in under 60 seconds.

SOAR + EDR Automation Project: LimaCharlie & Tines
This project demonstrates a complete Security Orchestration, Automation, and Response (SOAR) workflow integrated with Endpoint Detection and Response (EDR) using LimaCharlie for detection and Tines for automation. A Windows 11 VM simulates an endpoint where LaZagne malware triggers custom detections, leading to Slack alerts, analyst approval, and automated isolation.
​
​

Project Overview
The workflow begins with planning via a high-level diagram, followed by endpoint setup, agent deployment, detection rule creation, alert routing to Slack, human approval, and rapid isolation. LimaCharlie provides real-time EDR visibility and YAML-based detections, while Tines handles no-code automation across tools like Slack and LimaCharlie APIs.
​
​

Key technologies:

LimaCharlie: Cloud-native EDR with custom rules, real-time telemetry, and response actions like isolation.
​

Tines: SOAR platform for building workflows that ingest webhooks, notify teams, and execute API calls.
​

LaZagne: Credential dumping tool used for testing (MITRE ATT&CK T1003: OS Credential Dumping).
​

Step 1: Project Planning
Created a workflow diagram to outline the end-to-end process from detection to response.

<img width="834" height="807" alt="image" src="https://github.com/user-attachments/assets/d56b10ed-70ed-4e62-9b50-c23718fd0814" />

​

Step 2: Endpoint Setup
Deployed a Windows 11 VM on Vultr with RDP enabled and firewall rules allowing LimaCharlie/RDP traffic. Applied basic hardening for realistic testing.

<img width="1552" height="709" alt="image" src="https://github.com/user-attachments/assets/715853bd-127b-4c0c-977d-2d0619e9724f" />

​

Step 3: LimaCharlie Agent Deployment
Installed the LimaCharlie agent on the VM to enable telemetry ingestion and add it to the organization's sensors.
​
<img width="1108" height="581" alt="image" src="https://github.com/user-attachments/assets/6f735da8-18ed-485d-9c5f-0c927c1ceba1" />

<img width="1161" height="704" alt="image" src="https://github.com/user-attachments/assets/d9741d80-f2d8-4194-8c45-81f91e5858ee" />

​

Downloaded and executed LaZagne.exe to generate test events.

<img width="995" height="833" alt="image" src="https://github.com/user-attachments/assets/00915072-33a6-4378-9bda-ace73587299d" />

​

Step 4: Custom Detection Rule
Authored a YAML detection rule targeting lazagne.exe processes for credential access attempts. Tested the rule in LimaCharlie's console before deployment.

<img width="1203" height="863" alt="image" src="https://github.com/user-attachments/assets/df957130-e471-4729-adec-5b2cb00e7521" />

​​

Re-executed LaZagne to trigger the live detection.

<img width="1521" height="779" alt="image" src="https://github.com/user-attachments/assets/541b8152-05fa-4d12-aed3-216017df193e" />

​

Step 5: Tines Slack Alerts
Tines Story 1: Configured a workflow to receive LimaCharlie webhooks, extract key details (e.g., endpoint ID, detection name, timestamp), and post formatted alerts to Slack.

<img width="1184" height="617" alt="image" src="https://github.com/user-attachments/assets/d7673ff5-7f77-44b2-9ca3-19f9076efa72" />

<img width="1456" height="388" alt="image" src="https://github.com/user-attachments/assets/bfb868a3-9856-488e-bd09-491bbd06c042" />


​
​

Step 6: Analyst Approval
Tines Story 2: Built an interactive form for analysts to review alerts and approve actions like isolation.

<img width="577" height="523" alt="image" src="https://github.com/user-attachments/assets/745b81c0-997d-44d5-a701-6655a0cc2e56" />

​

Step 7: Automated Isolation
Upon approval, Tines called the LimaCharlie API to isolate the endpoint. Verified success with ping tests showing 100% packet loss to external hosts like google.com.

<img width="410" height="287" alt="image" src="https://github.com/user-attachments/assets/07133aed-373d-4e24-93c1-e9284265f95a" />

<img width="597" height="237" alt="image" src="https://github.com/user-attachments/assets/a601e1b2-def7-425a-af06-609313944723" />
​
​

Key Learnings and Future Enhancements
Benefits: Achieved sub-second detection-to-response, reducing MTTR via automation.
​

Scalability: Tines workflows scale without code; LimaCharlie supports open rulesets like Sigma.
​



