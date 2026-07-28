# Network Intrusion Detection System (NIDS) Lab
pfSense | Suricata | Kali Linux

##  Project Overview
This project details the build and configuration of an isolated home/virtual lab designed to perform network traffic inspection and threat detection. Using pfSense as the perimeter gateway and Suricata as an inline Intrusion Detection/Prevention System (IDS/IPS), this lab simulates attack vectors launched from a Kali Linux instance to evaluate signature-based detection and logging capabilities.

---

##  Network Architecture

* Hypervisor: Oracle VM VirtualBox
* Firewall / Gateway: pfSense 2.7.2 (Dual-Interface Setup)
  * em0: WAN Interface (NAT / Internet Connectivity)
  * em1: LAN Interface (Isolated Internal Network `192.168.1.1/24`)
* Intrusion Detection Engine: Suricata bound to em1 (LAN)
* Attacker System: Kali Linux (Reconnaissance & Penetration Testing)

---

##  Key Technical Implementations & Configuration

### 1. pfSense Network Deployment
* Configured dual network interfaces (`em0` for WAN routing and em1 for internal LAN traffic isolation).
* Set up internal DHCP services to dynamically assign IP addresses to internal network clients.

### 2. Suricata IDS Integration
* Installed Suricata on pfSense via package management.
* Configured Global Settings to pull live signature rulesets (Emerging Threats Open rulesets).
* Bound the Suricata inspection engine directly to the em1 LAN interface to monitor internal and outbound packet traffic.
* Validated engine status, pattern matching algorithms, and rule synchronization logs.

---

##  Engineering & Troubleshooting Log

Building this lab involved resolving several real-world network and OS deployment obstacles:

* Repository & Dependency Issues: Resolved FreeBSD pkg repository errors and PHP version mismatched dependencies on pfSense by temporarily adjusting routing and NAT adapters to guarantee stable outbound traffic.
* DNS & Routing Resolution: Fixed host-level DNS resolution issues, ensuring the pfSense system could consistently update Suricata signature definitions from external feeds.

---
##  Screenshots & Evidence

* docs/suricata-interface.png — Suricata engine status active and bound to the LAN (`em1`) interface.
* docs/nmap-simulation.png — Reconnaissance and OS detection scan executed from Kali Linux targeting the gateway.

##  Threat Simulation & Detection Workflow

1. Reconnaissance: Execute network discovery scans (`nmap -sS -sV -O`) from Kali Linux against internal assets.
2. Packet Inspection: Suricata inspects incoming frames against active signature rulesets in real time.
3. Alert Analysis: Observe, analyze, and document trigger events via the Suricata Alerts tab and /var/log/suricata/ logs.

---

##  Key Takeaways
* Practical experience in network segmentation, interface binding, and firewall rulesets.
* Hands-on exposure to signature-based intrusion detection systems (IDS).
* Improved system troubleshooting skills across FreeBSD routing, package management, and DNS stack configurations.
