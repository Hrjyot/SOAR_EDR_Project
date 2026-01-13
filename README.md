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

<img width="834" height="807" alt="Untitled Diagram drawio" src="https://github.com/user-attachments/assets/fafcb2fd-1aeb-493d-9fba-84aba645097e" />


​

Step 2: Endpoint Setup
Deployed a Windows 11 VM on Vultr with RDP enabled and firewall rules allowing LimaCharlie/RDP traffic. Applied basic hardening for realistic testing.

<img width="1552" height="709" alt="2026-01-09T18_52_53" src="https://github.com/user-attachments/assets/85b56ae8-add5-464a-9623-98384d2d8250" />


​

Step 3: LimaCharlie Agent Deployment
Installed the LimaCharlie agent on the VM to enable telemetry ingestion and add it to the organization's sensors.
​
<img width="1108" height="581" alt="2026-01-09T18_51_54" src="https://github.com/user-attachments/assets/f678ae5d-b9fd-4594-934b-e7d3dcbdcf0a" />


<img width="1279" height="710" alt="2026-01-12T15_27_08" src="https://github.com/user-attachments/assets/e7ab20e3-757f-4f0a-a552-396642255b5b" />


​

Downloaded and executed LaZagne.exe to generate test events.

<img width="995" height="833" alt="2026-01-12T15_45_57" src="https://github.com/user-attachments/assets/c58de5d3-3b23-49b8-9bac-76c14582c6f2" />


​

Step 4: Custom Detection Rule
Authored a YAML detection rule targeting lazagne.exe processes for credential access attempts. Tested the rule in LimaCharlie's console before deployment.

<img width="1191" height="733" alt="2026-01-12T16_10_24" src="https://github.com/user-attachments/assets/38d47dfa-b17d-4c9b-b23c-5fe763d47e5b" />


​​

Re-executed LaZagne to trigger the live detection.

<img width="1612" height="841" alt="2026-01-12T16_14_35" src="https://github.com/user-attachments/assets/03b766b4-e966-4644-82d4-99a94bc70501" />


​

Step 5: Tines Slack Alerts
Tines Story 1: Configured a workflow to receive LimaCharlie webhooks, extract key details (e.g., endpoint ID, detection name, timestamp), and post formatted alerts to Slack.

<img width="1184" height="617" alt="2026-01-12T20_09_21" src="https://github.com/user-attachments/assets/69022d5f-8da1-4077-9373-1b5816f3a6d3" />


<img width="1456" height="388" alt="2026-01-12T19_58_04" src="https://github.com/user-attachments/assets/f44871e0-c1b4-481b-af72-344c00ccf65f" />



​
​

Step 6: Analyst Approval
Tines Story 2: Built an interactive form for analysts to review alerts and approve actions like isolation.

<img width="577" height="523" alt="2026-01-12T19_53_59" src="https://github.com/user-attachments/assets/b8e6bc45-6499-4675-88ed-10da2d1f1c6c" />


​

Step 7: Automated Isolation
Upon approval, Tines called the LimaCharlie API to isolate the endpoint. Verified success with ping tests showing 100% packet loss to external hosts like google.com.

<img width="410" height="287" alt="2026-01-12T19_55_14" src="https://github.com/user-attachments/assets/17003cf7-93ec-40da-b6df-bc37fdcfca8e" />


<img width="597" height="237" alt="2026-01-12T19_57_52" src="https://github.com/user-attachments/assets/03b89216-cc26-4b4c-8d8a-ce6f3bb1f31a" />

​
​

Key Learnings and Future Enhancements
Benefits: Achieved sub-second detection-to-response, reducing MTTR via automation.
​

Scalability: Tines workflows scale without code; LimaCharlie supports open rulesets like Sigma.
​



