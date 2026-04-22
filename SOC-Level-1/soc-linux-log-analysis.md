# SOC Network Security Investigation — Linux Log Analysis (Beginner Project)

## Overview

This project demonstrates how Security Operations Center (SOC) analysts investigate network attacks using **Linux command-line tools**. It is based on real-world-style scenarios involving firewall logs, IDS alerts, and VPN authentication logs.

The goal is to understand how attackers move through a network — from reconnaissance to compromise — using only **log analysis and Linux commands**.

---

## Objectives

* Understand network visibility in cybersecurity
* Differentiate external vs internal scanning
* Identify brute-force attacks in VPN logs
* Detect lateral movement using SMB (port 445)
* Track C2 (Command & Control) communication
* Identify data exfiltration attempts
* Use Linux commands to extract security insights

---

## Tools Used

* Linux terminal (Ubuntu)
* `cat`
* `grep`
* `cut`
* `sort`
* `uniq`
* `head`
* CSV log files (firewall, IDS, VPN logs)

---

## Attack Scenario Breakdown

### 1. Reconnaissance (External Scanning)

Attackers scan the network perimeter looking for open ports and services.

```bash
cat firewall.log | grep "BLOCK" | head
```

 Identifies repeated connection attempts to multiple ports (SSH, FTP, RDP, SMB)

---

### 2.  Brute Force Attack (VPN Access)

Attackers attempt multiple logins until one succeeds.

```bash
cat vpn_auth.log | grep "FAIL"
```

```bash
cat vpn_auth.log | grep "SUCCESS"
```

 Shows repeated failed login attempts followed by successful authentication

---

### 3. Internal Access Granted

After successful login, attacker receives an internal IP (VPN-assigned address).

```text
assigned_ip=10.8.0.23
```

 This confirms initial access inside the network

---

### 4. Lateral Movement (SMB / Internal Scanning)

Attacker scans internal systems using SMB (port 445), SSH (22), and RDP (3389).

```bash
cat firewall.log | grep "445"
```

```bash
cat firewall.log | grep "ALLOW"
```

 Indicates movement between internal machines

---

### 5.  Command & Control (C2 Beaconing)

Compromised host communicates with external attacker server at regular intervals.

```bash
cat ids_alerts.log | grep "C2"
```

 Shows periodic beacon traffic (commonly port 4444)

---

### 6.  Data Exfiltration

Large outbound traffic detected indicating possible data theft.

```bash
cat firewall.log | grep "POST"
```

```bash
cat ids_alerts.log | grep "Data Exfiltration"
```

👉 Confirms sensitive data being sent outside the network

---

## Key Findings

* External IP performed reconnaissance scans
* VPN credentials were brute-forced successfully
* Attacker gained internal network access
* Lateral movement detected via SMB (port 445)
* C2 communication established (port 4444)
* Data exfiltration attempts confirmed

---

##  Key SOC Concepts Learned

* Network perimeter monitoring
* Log correlation (firewall + VPN + IDS)
* Attack lifecycle (MITRE ATT&CK mapping)
* Brute-force detection patterns
* Lateral movement identification
* C2 detection through behavioral analysis

---

## ⚡ Key Linux Command Patterns Used

### Find suspicious activity

```bash
grep "BLOCK"
grep "FAIL"
grep "SUCCESS"
```

### Extract specific fields

```bash
cut -d' ' -f5
```

### Sort and count occurrences

```bash
sort | uniq -c
```

### Filter top results

```bash
head
```

---

##  What This Project Demonstrates

This project simulates a real SOC investigation workflow where analysts:

* Start from raw logs
* Identify anomalies
* Correlate multiple data sources
* Reconstruct a full attack timeline

---

## Conclusion

Even without advanced tools, SOC analysts can detect full-scale cyber attacks using **basic Linux commands and log correlation techniques**. Understanding patterns in logs is a core cybersecurity skill for entry-level SOC roles.

##
