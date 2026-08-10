#Honeypot-Based-Threat-Intelligence-SOC-Monitoring
Integrated Threat Intelligence, SOC Analysis & VAPT via AWS Cowrie Honeypot
An end-to-end cybersecurity project demonstrating the integration of Threat Intelligence, SOC Log Analysis, Vulnerability Assessment & Penetration Testing (VAPT), and Linux Infrastructure Hardening.

By deploying an isolated Cowrie Honeypot on AWS, this project captures live, real-world attacker tactics, techniques, and procedures (TTPs), parses the raw threat logs, emulates those exact attacks in a safe internal lab, and executes system remediation.

Architecture & Data Flow
[ LIVE INTERNET ]
       |
       |  (Inbound SSH Attacks - Port 22)
       v
+-------------------------------------------------------+
|  AWS PUBLIC CLOUD (Isolated VPC)                      |
|   - Cowrie Medium-Interaction Honeypot                |
|   - iptables Redirect (Port 22 -> 2222)               |
+---------------------------+---------------------------+
                            |
                            | (Raw JSON Logs: cowrie.json)
                            v
+-------------------------------------------------------+
|  SOC ANALYSIS LAYER                                   |
|   - Python & jq Log Parsing                           |
|   - IOC Extraction (Attacker IPs, Credential Wordlists)|
+---------------------------+---------------------------+
                            |
                            | (Threat Intelligence Feeds)
                            v
+-------------------------------------------------------+
|  INTERNAL PRIVATE LAB (Air-Gapped VAPT)               |
|                                                       |
|   [ Kali Linux Attacker ] ----(Nmap / Hydra / MSF)--->|
|                                                       |
|                                                       v
|                                           [ Target Machines ]
|                                           - Metasploitable2
|                                           - Target Ubuntu Server
|                                                       |
|                                                       v
|                                           [ System Hardening ]
|                                           - SSH Key Enforced
|                                           - Root Access Disabled
+-------------------------------------------------------+
