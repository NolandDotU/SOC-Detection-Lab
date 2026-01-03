# Mini SOC Lab - Wazuh on AWS

**Role1:** SOC Analyst (Blue Team)
**Role2:** Attacker on Kali Linux (Red Team)
**Focus:** Detection, Log Analysis, Incident Triage
**Platform:** AWS EC2 and Kali Linux as Attacker
**SIEM:** Wazuh (ELK Stack) & Suricata as a sensor

_______________________________________________
## Overview
This repository demonstates a realistic SOC Lab built on AWS using Wazuh as a detecter and analyzer for real attack activity such as _nmap_ or _curl_

The Project Simulates:
- An attacker performing reconnaissence attacks.
- A Linux server as a monitored endpoint.
- A SIEM will perfoming detection on the attack and start alerting based on what Suricata detect.
_______________________________________________
## Components
- **Wazuh Manager:** SIEM, Detection, Dashboard
- **Ubuntu Victim:** Monitored endpoint
- **Kali Linux:** Attack Simulation
- **AWS EC2:** Cloud Server
_______________________________________________

Okay, there will be a 4 phases that will be doing they're will be on each phases's folder **Disclaimer** that this project is just for educational and defensive security purposes only. All attacks were executed in a controlled lab enviroment of my own.
