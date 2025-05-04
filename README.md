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
## 2:- Allow RDP in Firewall:
  - **Windows Defender Firewall → Advanced Settings → Inbound Rules → Remote Desktop (TCP-In) → Enable**
## 3:- Create Test User
   - **net user victim Password123 /add**
![30-Days-SOC-Challenge-Beginner_Challenge#3_Day#11- Introduction to Incident Response md at main · 0xrajneesh_30-Days-SOC-Challenge-Beginner - Google Chrome 30-04-2025 11_14_57](https://github.com/user-attachments/assets/000b2c79-b052-4007-b1ca-0765dcb4b0da)

# 🎯Simulate the Attack
- **On Kali Linux: Install Hydra (if not installed):**
    - sudo apt update && sudo apt install hydra
 - **Prepare Wordlist: Use the existing list or create a custom one . I have created custom one.**
![30-Days-SOC-Challenge-Beginner_Challenge#3_Day#11- Introduction to Incident Response md at main · 0xrajneesh_30-Days-SOC-Challenge-Beginner - Google Chrome 30-04-2025 11_19_16](https://github.com/user-attachments/assets/3d228d29-9309-49de-8bde-a2e1fb34bd82)
- ## Launch the bruetforce attack by the wordlist which we created.
- **hydra -l victim -p passwordlist.txt rdp://(windows server ip)**
![kali - VMware Workstation 16 Player (Non-commercial use only) 30-04-2025 11_25_47](https://github.com/user-attachments/assets/4c3256de-2b07-4c0a-ae57-116afd918ed1)
## 👁️Visualize the Alert in Event Viewer
- **1:- On Windows Server: Open Event Viewer → Windows Logs → Security**
- **2:- Look for Event ID 4625 with**
- **3:- Logon Type: 10 (RemoteInteractive / RDP)**
  - **Failure Reason: "Unknown user name or bad password"**
  ![kali - VMware Workstation 16 Player (Non-commercial use only) 30-04-2025 11_26_56](https://github.com/user-attachments/assets/7170213a-9eb7-4ca5-9874-eb46bb027a24)

# 🚨Incident Response Steps
- **1:- Identify Repeated Failed Logons:**
- **Spot Event ID 4625 from same IP**
- **2 Correlate IP Address:**
   - **Confirm repeated failures from attacker’s IP**
- **3:- Lock the User Account (Optional):**
    - **net user victim /active:no**
## Block Ip
- **Create a custom firewall rule to block the ip address of the attacker**
- **Go to a firewall->Advance Settings->inbound rule and click on the custom**
![Day#11- Incident Response Basics - YouTube - Google Chrome 30-04-2025 11_39_33](https://github.com/user-attachments/assets/0dedd5e2-effb-4fd5-9739-094ecc8b4711)

![windows server - VMware Workstation 16 Player (Non-commercial use only) 30-04-2025 11_40_10](https://github.com/user-attachments/assets/0698c649-cad9-4ffa-a142-999fbabe01ad)
- **Define the port which we want to block which is (3389) RDP port**
![Day#11- Incident Response Basics - YouTube - Google Chrome 30-04-2025 11_41_27](https://github.com/user-attachments/assets/41fcd0b3-f099-4743-a71a-893f8d966f4f)
- **define which remote ip this rule apply to which is our attacker kali machine**
![windows server - VMware Workstation 16 Player (Non-commercial use only) 30-04-2025 11_42_23](https://github.com/user-attachments/assets/e6595f89-c31c-4c14-8278-0027c283c9a6)

![windows server - VMware Workstation 16 Player (Non-commercial use only) 30-04-2025 11_43_36](https://github.com/user-attachments/assets/53aff2c8-345b-4eb1-8f20-2ad6f7f0eb5e)

- **check if ip is blocked or not**
- **we are going to use nmap to check ip is filtered or not**
![windows server - VMware Workstation 16 Player (Non-commercial use only) 30-04-2025 11_45_20](https://github.com/user-attachments/assets/360c00e9-645f-4884-a235-5fc09edf1eed)

- **we can also see the logs in generated by the firewall**
- **Right click on windows firewall Go to public profile->click on customization->copy the path**
![Day#11- Incident Response Basics - YouTube - Google Chrome 30-04-2025 11_48_39](https://github.com/user-attachments/assets/24f2a2fc-f67d-4c42-8840-ae75271a53e4)
- **paste the path in file manager**
![kali - VMware Workstation 16 Player (Non-commercial use only) 30-04-2025 11_55_33](https://github.com/user-attachments/assets/a85e89f5-4686-4e7c-91d2-2643761e71dc)

# ✅Conclusion
This lab demonstrated how to:
- **Simulate an RDP brute-force attack using Hydra**
- **Detect suspicious logons via Windows Event Viewer**
- **Respond with basic IR steps without using Sysmon**



  









   





