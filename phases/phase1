# PHASE 1

## OBJECTIVE
Deploying a cloud-based SIEM and preparing endpoints for monitoring.

**_______________________**
## AwS EC2 SETUP
### Instance (the components)
- **Wazuh Manager:** Ubuntu 24.04, or latest (m7i-flex.large)
- **Victim:** Ubuntu 24.04, or latest (t3.micro)
- **Attacker:** Kali Linux
**_______________________**

## Wazuh Installation (on Wazuh Manager Server)
from official Wazuh Installation

so we just pick the `Wazuh-install.sh` file with
`curl -sO https://packages.wazuh.com/4.11/wazuh-install.sh`
and we can just execute it with `sudo bash ./wazuh-install.sh -a`	

wait for a minutes, when it installed, at the on your terminal it will print a `User: admin` and a `Password`. Copy it for login into the Wazuh on browser with `https://IP-PUBLIC-OF-WAZUH-SERVER` and save it for later.

move to **Victim POV** for preparing the Wazuh Agent
1. Go to the Wazuh Dashboard
2. Click "Add Agent".
3. OS: Lunix - Deb/Ubuntu
4. Enter the Private IP of the Wazuh Manager.
5. Group: default
6. Run `wget https://packages.wazuh.com/4.x/wazuh-agent_...deb && sudo WAZUH_MANAGER='<MANAGER_PRIVATE_IP>' dpkg -i ./wazuh-agent_*.deb`
7. And Start it!
`sudo systemctl daemon-reload`
`sudo systemctl enable wazuh-agent`
`sudo systemctl start wazuh-agent`

if there's no error, you should be seeing "Total Agents: 1" on your Wazuh Dashboard, means we successed and we can go to setup the Suricata as a censor that detects networks attacks and forward it to the Wazuh
1. **Install Suricata**
