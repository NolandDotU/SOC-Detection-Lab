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
**1. Install Suricata**
```
sudo add-apt-repository ppa:oisf/suricata-stable
sudo apt update
sudo apt install suricata -y
```

**2. Check the Network Interface of the Victim (on Victim SSH)**
`ip -c a`
_for example mines are `ens5`_

**3. After knowing the Network Interface now we configure the config file**
`sudo nano /etc/suricata/suricata.yaml`
- in your nano search for `af-packet`. Look for line that says `- interface:` on that line change the value into the exact Network Interface on the Victim.
- Enabling the Community ID. Search line for `community-id`. Change the value into `true` if it still `false`.(So this step is to helps Suricata to match with alerts with Zeek or other tools).

**4. After finishing config and editing with update the Suricata Rules**
`sudo suricata-update`

**5. Just for testing the config if there's no error**
`sudo suricata -T -c /etc/suricata/suricata.yaml -v`
(if there's an error, search on the internet or text me)

**6. Start it!**
``sudo systemctl enable suricata
sudo systemctl restart suricata``

it works?

## Now movin on to **connect Suricata to Wazuh Agent** (the Victim)
**1. Edit the config file of Wazuh Agent**
`sudo nano /var/ossec/etc/ossec.conf`

**2. Add log collector line in it**
put it on the bottom so you dont get confuse? maybe
```
<localfile>
  <log_format>json</log_format>
  <location>/var/log/suricata/eve.json</location>
</localfile>
```
**3. Save and Exit and Restart the Wazuh**
`sudo systemctl restart wazuh-agent`

# DONE!!
Now all setup are completed, we can move to the phase 2 for attack simulation... bye
