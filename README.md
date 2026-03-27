# 🦈 Network Forensics: PCAP Analysis & Cleartext Interception

## 📝 Overview
This project simulates a **Network Forensics** investigation focusing on the vulnerabilities of unencrypted (Cleartext) communication protocols. Using a combination of command-line packet sniffing and GUI-based protocol analysis, I demonstrated how easily credentials can be extracted from network traffic if secure protocols (like SFTP/HTTPS) are not enforced.

---

## 🛠️ Tools & Environment
* **Platform:** Kali Linux
* **Packet Sniffing:** `tcpdump`, `netcat` (nc)
* **Protocol Analyzer:** `Wireshark`
* **Target Protocol:** FTP (File Transfer Protocol - Port 21)

---

## 🚀 Execution & Forensic Methodology

### Phase 1: Traffic Simulation & Capture (`tcpdump`)
To create a realistic scenario, I initiated a packet capture on the local loopback interface targeting port 21. Simultaneously, I used `netcat` to act as a mock FTP server and transmitted simulated credentials across the network.

![network_forensics](https://github.com/user-attachments/assets/3be0e54f-af90-4dfd-b9a9-41302bd657ce)

*Setting up the local packet capture and transmitting mock credentials via netcat.*

### Phase 2: Packet Analysis (`Wireshark`)
The resulting `.pcap` file was loaded into Wireshark. By applying the `ftp` display filter, I isolated the authentication sequence from the overall traffic dump.

### Phase 3: Intelligence Extraction
Because the FTP protocol does not utilize Transport Layer Security (TLS), the payload data is not encrypted. By inspecting the File Transfer Protocol layer in Wireshark, the exact credentials transmitted over the wire were easily readable.

![wireshark_passwd](https://github.com/user-attachments/assets/fa230103-5eb6-463c-aea4-2e30a6ff2d3d)

*Wireshark packet details showing the intercepted Username and Password in cleartext.*

---

## 🛡️ Remediation & Security Posture
This lab highlights a critical vulnerability in legacy enterprise configurations. 
* **Deprecation:** Cleartext protocols (FTP, Telnet, HTTP) must be deprecated.
* **Encryption:** Implement secure alternatives such as **SFTP** (SSH File Transfer Protocol) or **FTPS** (FTP over SSL/TLS) to ensure that packet sniffing yields only encrypted, unreadable cipher text.
