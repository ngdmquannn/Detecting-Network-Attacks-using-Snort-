# Network Attacks Detection using Snort

**Final project for the course _Applied Operating Systems**

This repository contains my final project where I implemented an Intrusion Detection System (IDS) using **Snort**. The project evaluates Snort’s ability to detect both network-level and application-level attacks in different deployment environments.  

Through this project, I applied knowledge of:
- **Operating systems** — Linux VM setup and service configuration  
- **Networking** — addressing, routing, DHCP, NAT, and port forwarding  
- **Security** — IDS operation, Snort rules, and attack simulation  

The work demonstrates how these areas combine to design, configure, and validate a functional IDS.

---

## 🖥️ VM Setup
The lab was built using **Kali Linux virtual machines** with different roles and NIC configurations.

### 🔹 Basic Lab

| VM Name       | Role                               | NICs                     |
|---------------|-----------------------------------|--------------------------|
| `kali-web`    | Web server + Snort (basic setup)  | Host-only  |
| `kali-attacker` | Attacker machine                 | Host-only |

- **Web Server + Snort VM** — hosts DVWA and runs Snort for monitoring.  
- **Attacker VM** — generates traffic and performs simulated attacks.  
- Both VMs are on the same internal network to emulate local attacks.  

### 🔹 Advanced Lab

| VM Name       | Role                               | NICs                     |
|---------------|-----------------------------------|--------------------------|
| `kali-attacker` | Attacker machine                 | NAT                     | 
| `kali-router` | Router + Snort (advanced setup)   | 1 NAT + 1 Host-only      |
| `kali-victim` | Target web server (DVWA)          | Host-only                | 

- **Router + Snort VM** — acts as a perimeter device, running Snort, DHCP, NAT, and port forwarding.  
- **Victim Web Server VM** — hosts DVWA inside the protected LAN.  
- **Attacker VM** — external machine launching attacks against the internal server.  
-  Router bridges external and internal networks, providing a realistic perimeter monitoring scenario, detecting the attacks before it entered the LAN.  

---

## ⚙️ Configuration Approach

### Basic Objective
- Deploy Snort on the web server to monitor local/internal traffic.  
- Define monitored network range to represent the host’s environment.  
- Create simple detection rules to identify:  
  - ICMP traffic (ping and flood)  
  - SYN flood attempts on common services  
- Validate that Snort alerts trigger correctly when attacker generates traffic.  

### Advanced Objective
- Deploy Snort on a router to monitor traffic between external attackers and internal hosts. Listening on the outside/inside network interfaces based on the objectives of the admin, this topic will be further discussed in the attached report.  
- Configure the router with:  
  - DHCP to serve internal clients  
  - IP forwarding to allow routing  
  - NAT and port forwarding for exposing internal services  
- Create targeted rules to detect:  
  - ICMP activity and floods directed at internal servers  
  - SYN flood attacks from external sources  
  - SSH connection attempts on forwarded ports  
  - SQL injection attempts against web applications  
- Validate that Snort generates alerts at the network perimeter, accounting for NAT and translated traffic.  

---

## 🔥 Attacks Demonstrated
- **ICMP Ping & Flood** — basic reconnaissance and denial-of-service.  
- **SYN Flood (hping3)** — volumetric TCP connection-exhaustion.  
- **SSH Connection Attempts** — detection of external access to internal services via port forwarding.  
- **SQL Injection** — detection of malicious payloads targeting a vulnerable web application.  

---

## 📂 Repository Contents
- **`24560015_Report.pdf`** — Complete report including theory, lab setup, configurations, rules, and results.  
- **Demo Videos** — Two recordings showing the attacks and Snort detections in real time.  
- **`README.md`** — This summary overview.  

---

## ✅ Conclusion
This project demonstrates how Snort can be effectively deployed in both host-level and perimeter environments to detect common network and application-layer attacks. By combining operating system configuration, network services, and custom Snort rules, the IDS was able to identify different attack types in realistic scenarios.  

The work emphasizes that **effective intrusion detection depends not only on rules, but also on correct placement of the IDS and careful network configuration**.  

---
