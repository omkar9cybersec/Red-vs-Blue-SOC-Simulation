
# 🛡️ Enterprise SOC & Active Defense Simulation

## 📌 Project Overview
This project simulates a real-world, distributed Enterprise Security Operations Center (SOC). Our team built a fully functional Cyber Range across a Zero-Trust network overlay, enabling us to simulate advanced Red Team attacks and engineer automated Blue Team defense mechanisms (Active Defense) in real-time.

Unlike traditional local labs, this infrastructure was completely distributed and connected via a mesh VPN, mimicking modern remote-work corporate environments.

## 🏗️ Architecture & Network Topology
The lab is built on a decentralized model using **Tailscale** to create a secure, flat mesh network uniting geographically separated Virtual Machines into a single corporate subnet (`100.x.x.x`).

* **Security Brain:** Ubuntu Server (Hosting Wazuh SIEM Manager)
* **Corporate Endpoints (Targets):** * Windows Server 2019 (Active Directory/RDP environment)
  * Metasploitable 3 / CentOS (Vulnerable Linux infrastructure)
* **Attacker Node:** Kali Linux

## 🛠️ Technology Stack
* **SIEM & XDR:** Wazuh Manager, Wazuh Agents
* **Offensive Tools (Red Team):** Kali Linux, Metasploit Framework, Nmap, Hydra
* **Networking:** Tailscale (Zero-Trust VPN)
* **Scripting & Automation:** Bash, PowerShell, Wazuh Active Response XML

## ⚔️ Simulation Phases

### 🔴 Phase 1: Offensive Operations (Red Teaming)
The Red Team acted as external threat actors targeting the corporate network:
1. **Reconnaissance:** Conducted deep network scans using `Nmap` to identify open ports, services, and OS versions on both Windows and Linux endpoints.
2. **Exploitation:** Utilized the `Metasploit Framework` to exploit known vulnerabilities (e.g., legacy FTP/Tomcat flaws) on the Metasploitable 3 server.
3. **Credential Harvesting:** Executed aggressive SSH and RDP brute-force attacks against the Windows Server 2019 and Linux servers using `Hydra` and custom wordlists (`rockyou.txt`).

### 🔵 Phase 2: Active Defense (Blue Teaming)
The Blue Team acted as SOC Analysts, focusing on detection and automated mitigation:
1. **Log Ingestion:** Configured Wazuh Agents to stream system logs, Windows Event Logs (Sysmon), and authentication attempts to the central Wazuh Manager.
2. **Rule Creation:** Tuned default Wazuh rules to reduce false positives and create high-fidelity alerts for brute-force attempts and suspicious network mapping.
3. **Automated Mitigation (The Climax):** Engineered **Active Response** scripts within Wazuh. When the SIEM detected 5 consecutive failed SSH/RDP login attempts from a specific IP, it automatically executed a script to drop the attacker's IP at the endpoint's firewall (iptables/Windows Defender Firewall) for a 10-minute timeout period, effectively shutting down the Red Team's attack in real-time.

## 🚀 Key Learning Outcomes
* Practical experience in SIEM deployment and endpoint monitoring.
* Deep understanding of how network attacks look from a defender's perspective (log analysis).
* Translating manual incident response into automated security playbooks (SOAR concepts).
* Managing cross-platform security (Windows Server & Linux).

