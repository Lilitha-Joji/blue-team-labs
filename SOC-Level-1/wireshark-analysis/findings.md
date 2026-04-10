# Wireshark Investigation – SOC Level 1 Findings

## Overview
This document contains packet analysis findings from Wireshark lab exercises. The goal is to identify and correlate network traffic patterns, detect anomalies, and understand potential malicious activity.

---

## 1. TCP Connect Scan Detection

### Filter Used
- tcp.flags.syn == 1
- tcp.flags.ack == 0
- tcp.window_size <= 1024

### Observation
TCP SYN packets were identified using the applied filter. These packets represent initial connection attempts where the TCP handshake is not completed.

### Result
- Total TCP Connect scans detected: 1000

### Analysis
The high volume of SYN packets without corresponding ACK responses indicates automated scanning behavior. This is consistent with port scanning or reconnaissance activity targeting multiple ports.

### Conclusion
The traffic suggests a TCP Connect scan was performed against the target system. This indicates possible pre-attack reconnaissance activity.

---

## 2. ICMP Port Unreachable Detection

### Filter Used
- icmp.type == 3 and icmp.code == 3

### Observation
ICMP Destination Unreachable (Port Unreachable) messages were observed. These responses indicate that UDP packets were sent to ports that are not actively listening on the target system.

### Result
- Total ICMP Port Unreachable messages: 1083

### Analysis
The high number of ICMP responses suggests repeated attempts to access closed UDP ports. This behavior is commonly associated with UDP port scanning or network reconnaissance activity.

### Conclusion
The traffic indicates potential UDP port scanning activity, where multiple closed ports responded with ICMP unreachable messages.

---
