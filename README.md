# Wazuh-Lab-Documentation
Documentation of my Wazuh SIEM lab using Ubuntu Manager and Windows Agent
# Wazuh Lab – Ubuntu Manager with Windows Agent

## Introduction

This project sets up a **Wazuh SIEM lab** using an Ubuntu VM as the Wazuh Manager and my own Windows computer as the agent.
The goal is to practice security monitoring, log analysis, and alert management in a hands-on way.

---

## Step 1: Install Wazuh Manager on Ubuntu

Update and upgrade:

```bash
sudo apt update && sudo apt upgrade -y
```

Install Wazuh:

```bash
curl -sO https://packages.wazuh.com/4.9/wazuh-install.sh
sudo bash wazuh-install.sh -a
```

---

## Step 2: Find Ubuntu VM IP

```bash
ip a
```

---

## Step 3: Install Wazuh Agent on Windows

Download the Windows agent from the [official site](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package.html#windows).

During setup:

* Manager IP → your Ubuntu VM IP
* Agent name → Windows hostname

---

## Step 4: Register Agent with Manager

On Ubuntu:

```bash
sudo /var/ossec/bin/manage_agents
```

* Add agent
* Copy the key

On Windows:

* Paste the key into `ossec.conf`
* Restart the **Wazuh Agent service**

---

## Step 5: Verify Connection

Check if the agent is active:

```bash
sudo /var/ossec/bin/agent_control -l
```

---

## Changing Wazuh Dashboard Password

```bash
sudo docker exec -it wazuh.dashboard bash
/var/ossec/wazuh-passwords-tool.sh --change admin
exit
sudo systemctl restart wazuh-dashboard
```

---

## Why Use My Own Windows as Agent

Using my daily Windows PC makes the lab realistic. I can monitor:

* Login attempts
* File changes
* Service activity
* Policy violations

---

## Next in the Series

* Part 2 – Adding Linux agents
* Part 3 – Simulating attacks and detections
* Part 4 – Custom dashboards and rules
* Part 5 – Automating responses

---

## Conclusion

This Wazuh lab is my starting point for hands-on cybersecurity monitoring. With Ubuntu as the manager and Windows as an agent, I now have a real-world setup for learning SIEM and detection.
