# PHASE 2

## OBJECTIVE
Detecting scanner from attacker and detecting repeated unauthorized SSH login attempts.

**_______________________**
## Attack Simulation
### From Kali Linux > Suricata (Detecting Activity) > Wazuh Agent (Read) > to dashboard of Wazuh Manager (Alert).
**_______________________**

**Note**
for Brute-force attack may not be a attempted due the SSH login must have the keypair.pem to avoid brute-force which make the server more secure than using password authentication.

oke soo for the brute-force may difficult to try but ill give the screenshot the result of me trying to brute-force it.

## OKAY, we do scan attack instead.
**1. Use the Suricata fastlog debugging for realtime**
`tail -f /var/log/suricata/fast.log`

**2. Launch the scan attack (From Kali Linux/Attacker)**
- `nmap -A -T4 Private/Public-IP-of-Ubuntu-Victim` or for specific test that Suricata hates (User-Agent scanning) `curl -A "BlackSun" http://Victim_IP`
- `hydra -l ubuntu -p testpass123 ssh://Victim-IP`

Okay now when both side your log and the attack or active, you can see the Suricata giving indicating alerting of someone/thing are scanning the port or the server.

**3. Finally we can view it on the Wazuh Dashboard**
1. Open the Wazuh Dashboard inthe browser
2. Go to Threat Hunting or Security Events
3. In the searchbar, type: `rule.groups:suricata`
4. And you should see alerts like `ET SCAN Nmap Scripting Engine User-Agent` or something similiar with it.

## Conclusion

This phase demonstates how **early-stage attacker activity** such as scanning and reconnaissance can be detected **before main exploitation happens**

By Correlation:
- Network alert censor(Suricata)
- System logs from Wazuh Agent
- Centralized monitoring through the Wazuh Dashboard

As a SOC analyst can quickly identify malicious intent and take preventive action.
Even if SSH Brute-force attacks were implemented by **forcing key-based authentication**, the visibility provided by Suricata and Wazuh still allows analyst to **detect an enumeration attempts**, which are often happens to real attacks.

This phase of defense, where secure configuration and simultanious monitoring work together to **reduce risk**.
