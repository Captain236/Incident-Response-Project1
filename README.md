# Incident-Response-Project1
# What is Incident Response?
**Incident Response (IR) is the structured approach to handle and manage the aftermath of a security breach or cyberattack, also known as an incident. It includes steps to:**
- **Detect the incident**
- **Contain the damage**
- **Investigate the root cause**
- **Recover normal operations**
- **Report and document findings**
# Incident Response Process (NIST SP 800-61 Rev. 2)
The NIST Incident Response Lifecycle includes 4 main phases:
| Phase                                | Description                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| 1. Preparation                       | Establish policies, train team, and set up tools and logging mechanisms.    |
| 2. Detection and Analysis            | Identify potential incidents using logs, alerts, and anomaly detection systems. |
| 3. Containment, Eradication, Recovery | Isolate threats, remove malware/artifacts, and restore systems securely.    |
| 4. Post-Incident Activity            | Conduct lessons learned, create reports, and improve incident response plans. |

# Common Types of Incidents Across Platforms
| Platform    | Common Incident Types                                                                 |
|-------------|----------------------------------------------------------------------------------------|
| Windows     | Malware infections, RDP brute-force attacks, unauthorized access, registry changes     |
| Linux       | SSH brute-force attacks, rootkit installation, file permission abuse, web defacement   |
| AWS         | Misconfigured S3 buckets, exposed credentials, unauthorized IAM activity, EC2 abuse    |
| Networks    | DDoS attacks, ARP spoofing, port scanning, unauthorized device connection              |

# How SOC Analysts Respond to Incidents:
- **Monitor logs and alerts (via SIEM)**
- **Investigate suspicious behavior**
- **Contain and isolate infected systems**
- **Coordinate with other teams**
- **Document and report the incident**

# 🧪 Lab Task: Detect and Respond: Windows Server RDP Brute Force Attack
# 🧰Lab Setup and Requirements
# 🖥️Machines Required:
## Windows Server 2019 or 2022
- **RDP enabled**
 **Event Viewer access**
- **One local user account with known username**
## Kali Linux VM
- **Hydra pre-installed**
- **Connected to same LAN or Virtual Network**
## 📶Network:
- **Ensure both machines are on the same network**
- **Verify RDP (TCP/3389) is open on Windows Server**
# ⚙️Preparation Steps
# On Windows Server:
## 1:- Enable RDP
   - **System Properties → Remote → Enable Remote Desktop**
![windows server - VMware Workstation 16 Player (Non-commercial use only) 30-04-2025 11_07_42](https://github.com/user-attachments/assets/bbd7cf2e-cb3b-412a-9a47-1ad7b1b8f453)




