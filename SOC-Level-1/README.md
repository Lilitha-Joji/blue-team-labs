# SOC Investigation – Multi-Stage Malware Analysis

## Overview
This project documents a multi-stage malware investigation conducted in a simulated SOC environment.  

The attacker continuously changed techniques to evade detection, requiring multiple defensive strategies including:
- Hash-based detection
- IP blocking
- DNS filtering
- Host-based detection (registry monitoring)

---

## Scenario
A simulated adversary repeatedly adapted their attack:

1. Initial malware identified through file hash  
2. Malware switched to direct IP-based communication  
3. Malware then used domain-based communication  
4. Final stage involved host-based persistence via registry changes  

---

## Investigation Stages

### Stage 1 – Hash-Based Detection
- Analyzed `sample1.exe` in the malware sandbox  
- Identified the file as malicious  
- Extracted SHA256 hash  
- Added hash to blocklist  

**Result:** Malware execution successfully blocked  

---

### Stage 2 – Firewall / IP-Based Detection
- Analyzed `sample2.exe`  
- Observed outbound connection to suspicious IP  
- Identified C2 server communication  
- Created egress firewall rule to block IP  

**Result:** Command-and-control (C2) communication stopped  

---

### Stage 3 – DNS-Based Detection
- Analyzed `sample3.exe`  
- Observed domain-based communication  
- Identified malicious domain:  
  `emudyn.bresonicz.info`  
- Implemented DNS filtering rule  

**Result:** Domain-based C2 communication blocked  

---

### Stage 4 – Host-Based Detection (Registry Analysis)
- Analyzed `sample4.exe`  
- Detected registry modification activity  
- Malware disabled Windows Defender real-time monitoring  

**Registry Key:**

HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Defender\Real-Time Protection

**Modified Value:**

DisableRealtimeMonitoring = 1

- Created Sigma rule to detect this behavior  

**Result:** Persistent detection of malware behavior achieved  

---

## MITRE ATT&CK Mapping

| Technique | Description |
|----------|------------|
| TA0005 | Defense Evasion |
| TA0011 | Command and Control |
| T1112 | Modify Registry |
| T1562.001 | Disable Security Tools |

---

## Key Takeaways
- Hash-based detection is fast but easily bypassed  
- IP blocking is effective but attackers can rotate IPs  
- DNS filtering provides stronger detection  
- Host-based detection (registry monitoring) is the most reliable  

---

## Skills Demonstrated
- Malware triage  
- Indicator of Compromise (IOC) analysis  
- Network traffic analysis  
- Firewall rule creation  
- DNS filtering implementation  
- Registry analysis  
- Sigma rule development  
- MITRE ATT&CK mapping  

---

## Tools Used
- PicoSecure Malware Sandbox  
- Firewall Rule Manager  
- DNS Filtering Engine  
- Sigma Rule Builder  
- Sysmon (conceptual)  

---

## Conclusion
This investigation highlights the importance of layered security in modern SOC operations.  

As attackers evolve their techniques, defenders must move beyond simple IOC-based detection and implement behavioral and host-based monitoring for effective threat detection and response.

## Adversary Evolution

During the investigation, the attacker adapted their techniques after initial detections were blocked.

A message from the adversary revealed:
- Introduction of a new sample: `sample5.exe`
- Shift of malicious logic to a backend server
- Reduced host-based indicators
- Increased reliance on network-based behavior

This forced a transition from:
- Static detection (hashes)
- Network indicators (IP/DNS)

 To behavioral detection strategies

This demonstrates real-world adversary adaptation and the need for layered defense.
