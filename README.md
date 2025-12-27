# SOC Brute-Force Attack Simulation and SOC Detection Lab

## **Overview**
This project demonstrates and **SSH brute-force attack simulation by Hydra or any brute-force tool** in a controlled lab enviroment and its **Detection from SOC Perspective**.

**The Goal:**
- Simulate a realistic basic attacker technique
- Generate authentication telemetry
- Validate that brute-force activity is logged and detectable
- Communicate findings in SOC-Friendly language

===============================================

## **Lab Architecture**
**Attacker (Red Team POV)**
- Kali Linux (my own laptop)
- Tool: Hydra

**Targer (Defender POV)**
- Ubuntu 24.04 Server (Using AWS EC2)
- OpenSSH
- Log source: `/var/log/auth.log`
- User: `evilcorp` (non-privilaged)

Kali (Attacker)
|
|SSH Brute Force with Hydra from port 22 
|
AWS EC2 UBuntu Server
|
|auth.log. So this is where the monitoring is, currently manual because depending automation and alerting implementation
|
SOC/SIEM Detection

===============================================

**Talk about ATTACK POV**
So here i use Hydra to Brute-force a SSH using just a simple password like on the screenshot using this command
`hydra -l evilcorp -p Password123 ssh://15.134.85.195`
So the objective/mission is to gain unauthorize SSH access by guessing credentials and generarte a multiple failed login attempts so we can see it on auth.log.

**Switch into DEFEND POV**
after the attacker did bruteforce or some failed attempt it will shows a log like this exemple (we can see it too on auth-log-failed.png screenshot)
`Failed password for evilcorp from 182.8.193.159 port 33308 ssh2`


**===DISCLAIMER===**
This project is created for **educational only and defensive purposes only.**
All attack were just performed by my own.
I did this just showing my skill and demonstrate it for writeing up without risking others
DO NOT attempt these techniques on systems without permission because you can get caught and that's really unethically.

**SKILL DEMONSTRATED**
- SOC Monitoring
- Log Correlation
- SSH Security Analyst
- MITRE ATT&CK Framework
- Incident Triage

  Thanks for reading this hopefully it useful for knowledges
  see u soon
