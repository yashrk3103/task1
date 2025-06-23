# 🔐 Network Port Scanning Task using Nmap

## 📝 Introduction

This project was part of a cybersecurity internship task that involved performing a basic port scan on a local network using **Nmap** on **Kali Linux**. The goal was to identify active IP addresses and open ports within the network subnet. The task also included analyzing the findings and documenting the process.

---

## 🌐 IP Range Scanned

```
192.168.1.0/24
```

This range was determined from my local machine's IP address: `192.168.1.17`

---

## 🔍 Key Findings

Below are the active hosts and the open ports identified:

```
192.168.1.1 - open ports: 53 (DNS), 80 (HTTP), 443 (HTTPS)
192.168.1.3 - open port: 7070 (RealServer)
192.168.1.17 - open port: 80 (HTTP)
```

These results indicate that:

* The default gateway (likely the router) is running DNS and web services.
* One host (192.168.1.3) is running a RealServer service on port 7070.
* My own machine (Kali) is serving a web server on port 80.

---

## 🔧 Common Services on Open Ports

| Port | Service    | Description                                |
| ---- | ---------- | ------------------------------------------ |
| 53   | DNS        | Domain Name System - resolves domain names |
| 80   | HTTP       | Web service - hosts websites               |
| 443  | HTTPS      | Secure web service (encrypted HTTP)        |
| 7070 | RealServer | Used by RealAudio streaming protocols      |

These are well-known ports and can expose essential services to users — or to potential attackers if left unsecured.

---

## ⚠️ Security Risks Identified

* **Port 80 and 443**: If the web service is outdated or misconfigured, it could be exploited through vulnerabilities (e.g., XSS, SQLi).
* **Port 53**: Open DNS can be abused for amplification attacks or data exfiltration.
* **Port 7070**: This less-common port may be overlooked, but streaming services can have unpatched flaws or weak auth.

To minimize risk:

* Disable unnecessary ports/services.
* Use firewalls to restrict traffic.
* Ensure all services are updated and monitored.

---

## 📷 Screenshots / Command Outputs

Scan command used:

```bash
sudo nmap -sS 192.168.1.0/24 -oN scan_result.txt
```

Result preview:

```text
Nmap scan report for 192.168.1.1
PORT     STATE SERVICE
53/tcp   open  domain
80/tcp   open  http
443/tcp  open  https

Nmap scan report for 192.168.1.3
PORT     STATE SERVICE
7070/tcp open  realserver

Nmap scan report for 192.168.1.17
PORT     STATE SERVICE
80/tcp   open  http
```

(Full results available in the attached `scan_result.txt` and `scan_result.html` files.)

---

## 💡 Optional Interview Questions

**1. What is an open port?**

> An open port is a communication endpoint that is actively accepting data from clients. Services and applications use open ports to send and receive data over the network.

**2. How does Nmap perform a TCP SYN scan?**

> Nmap sends a TCP SYN packet to each port. If the target replies with a SYN-ACK, the port is marked as open. If it replies with RST, the port is closed. If there is no response or an ICMP unreachable message, the port may be filtered.

**3. What risks are associated with open ports?**

> Open ports can expose services that might be vulnerable to exploitation if not properly secured. Attackers may use these ports to gain unauthorized access, launch denial-of-service attacks, or exploit known software vulnerabilities.

**4. Explain the difference between TCP and UDP scanning.**

> TCP scans establish or attempt to establish a connection, making it easier to confirm the status of a port. UDP scans send datagrams without a handshake and rely on ICMP responses, making them slower and less reliable. TCP scans are generally more accurate and faster.

**5. How can open ports be secured?**

> Open ports can be secured by:

* Closing unnecessary ports
* Using firewalls to restrict access
* Updating and patching services
* Using encryption and authentication where needed

**6. What is a firewall's role regarding ports?**

> A firewall monitors and controls incoming and outgoing traffic based on predefined security rules. It can block or allow access to specific ports to prevent unauthorized access or attacks.

**7. What is a port scan and why do attackers perform it?**

> A port scan is a method used to discover open ports and services on a host. Attackers perform port scans to map the attack surface, identify vulnerable services, and plan further exploitation.

**8. How does Wireshark complement port scanning?**

> Wireshark captures and displays raw network packets in real-time. It helps visualize Nmap activity, verify packet responses, analyze unexpected behavior, and detect anomalies or scanning attempts.

