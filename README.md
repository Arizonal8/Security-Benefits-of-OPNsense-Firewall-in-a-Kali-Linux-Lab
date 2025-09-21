# OPNsense Firewall Lab on VirtualBox

## 📌 Project Overview
This project demonstrates how to install and configure **OPNsense Firewall** in a virtualized lab environment using **VirtualBox**. The goal was to route all Kali Linux traffic through the OPNsense firewall, ensuring network segmentation, monitoring, and security enforcement.  

By setting up this environment, I created a controlled network where any traffic from Kali Linux must first pass through the OPNsense firewall before reaching the internet. This simulates a real-world security architecture where a firewall acts as the first line of defense against external threats.  

---

## 🛠️ Tools & Technologies
- **VirtualBox** – Virtualization platform  
- **OPNsense** – Open-source firewall & routing platform  
- **Kali Linux** – Security-focused Linux distribution for testing and monitoring  
- **PowerShell** – Used to download and extract the OPNsense image  

---

## 🔑 Steps Taken

### 1. Download & Extract OPNsense
- Downloaded the OPNsense installation image (`.bz2`) from the official website.  
- Used PowerShell with `bzip2` to extract the image for VirtualBox.  

### 2. Configure VirtualBox for OPNsense
- Created a new VM in VirtualBox for OPNsense.  
- Added **two network adapters**:  
  - **Adapter 1 (WAN)**: NAT (provides internet access to OPNsense).  
  - **Adapter 2 (LAN)**: Internal Network (`intnet`) for communication with Kali Linux.  

### 3. Configure OPNsense Interfaces
- Booted into OPNsense console and assigned interfaces:  
  - **WAN → em0 (DHCP)** → Receives internet from VirtualBox NAT.  
  - **LAN → em1 (192.168.1.1/24)** → Provides internal network for Kali Linux.  
- Disabled DHCP on LAN (manual IP assignment for Kali).  
- Confirmed Web GUI available at `https://192.168.1.1`.  

### 4. Configure Kali Linux Networking
- Configured Kali’s adapter to connect to the same Internal Network (`intnet`).  
- Manually assigned IP address in the OPNsense LAN subnet:  
  ```bash
  sudo ip addr add 192.168.1.10/24 dev eth0
  sudo ip route add default via 192.168.1.1
  ```
- Verified connectivity by pinging OPNsense:
  ```bash
  ping 192.168.1.1
  ```
- Accessed OPNsense Web GUI in Firefox using:  
  ```
  https://192.168.1.1
  ```

---

## ✅ Results
- Successfully established a virtual network where **all Kali Linux traffic flows through OPNsense**.  
- Verified firewall GUI access and network reachability.  
- Demonstrated the ability to control, monitor, and filter traffic.  

---

## 🔒 Security Advantages

1. **Network Segmentation**  
   - Separates internal traffic (Kali) from external internet access.  
   - Limits exposure of internal systems to direct attacks.  

2. **Traffic Filtering**  
   - OPNsense can enforce firewall rules to block malicious traffic.  
   - Example: Blocking known bad IPs, ports, or protocols.  

3. **Intrusion Prevention & Detection**  
   - OPNsense supports Suricata IDS/IPS to detect suspicious activity.  
   - Protects Kali from inbound/external attacks in the lab environment.  

4. **Logging & Monitoring**  
   - Centralized logs of all traffic leaving/entering the LAN.  
   - Useful for incident response and forensic analysis.  

5. **Realistic Simulation of Enterprise Security**  
   - Mirrors how corporate networks force all devices to connect through a firewall/gateway.  
   - Helps practice security monitoring, penetration testing, and SOC workflows.  

---

## 🚀 How This Mitigates Attacks
- Prevents **direct internet access** from Kali → forces all traffic through a controlled firewall.  
- Allows the application of **rules to block scanning, brute-force attempts, and malware communication**.  
- Enables the testing of **firewall policies, intrusion detection systems, and secure configurations** in a safe environment.  

---

## 📚 Learning Outcomes
- Hands-on experience with **firewall configuration**.  
- Understanding of **network interface assignments (WAN/LAN)**.  
- Practical knowledge of **routing traffic through security appliances**.  
- Ability to simulate real-world **network security architectures** in a lab environment.  

---

## 🔮 Future Improvements
- Enable **DHCP server** on LAN to dynamically assign IPs.  
- Integrate **IDS/IPS (Suricata)** for deeper packet inspection.  
- Add **VPN server on OPNsense** for secure remote connections.  
- Connect multiple client VMs (Windows/Linux) for multi-host network simulation.  

---

## 📌 Author
**Arinze Fortune Ihekweme**  
Cybersecurity Enthusiast | SOC & Cloud Security Learner  
