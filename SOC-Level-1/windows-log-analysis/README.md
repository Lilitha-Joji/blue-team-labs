Objective

Investigate Windows Security logs to identify:

Source of brute force attack
Compromised user account
Malicious RDP session Logon ID
Data Source
Windows Security Event Logs
Event IDs:
4625 → Failed logins
4624 → Successful logins
Attack Summary

A brute force attack was launched against the THM-PC, resulting in successful compromise of an administrator account and remote desktop access.

Findings
1. Brute Force Source IP

Repeated failed login attempts were observed targeting the system.

Event ID: 4625
Source IP: 10.10.53.248
Pattern: Multiple authentication failures (password spraying / brute force behavior)


2. Compromised User Account

The attacker successfully gained access to the system using a valid account.

Event ID: 4624
Account: Administrator
Result: Successful authentication after failed attempts


3. Malicious RDP Session

The attacker established a remote desktop session after successful authentication.

Event ID: 4624
Logon Type: 10 (RDP)
Logon ID: 0x183C36D
Source IP: 10.10.53.248
Attack Chain
4625 → Brute force attempts from 10.10.53.248
   ↓
4624 → Successful login (Administrator compromised)

User Management Events Investigation
Overview

This investigation focused on identifying suspicious account management activity inside the Windows Security Event Logs using the Practice-Security.evtx file.

The goal was to trace attacker actions after initial access and identify persistence mechanisms commonly used during ransomware and post-exploitation activity.

Key Findings
Suspicious Backdoor Account Created

Soon after a successful RDP login, a suspicious account was created:

svc_sysrestore

The naming convention resembles a legitimate Windows service account, which is a common attacker technique used to avoid suspicion.

Associated Event ID:

4720 — A user account was created
Privileged Group Membership Changes

The attacker added the backdoor account into two privileged groups:

Backup Operators
Remote Desktop Users

Associated Event ID:

4732 — A member was added to a security-enabled local group

This indicates:

persistence establishment
remote access capability
privilege escalation preparation
Log Correlation

The Logon ID field matched the previous successful RDP authentication event.

Result:

Yes

This correlation confirms that:

the same authenticated session performed the malicious account creation
the attacker used the active RDP session to establish persistence
Attack Flow Reconstruction

The following sequence was identified during analysis:

4624  → Successful RDP Login
4720  → Backdoor Account Created
4732  → Added to Privileged Groups
4624  → Potential Reuse of Backdoor Account

This pattern strongly resembles real-world post-compromise attacker behavior observed during ransomware intrusions and lateral movement operations.

Why This Activity Is Suspicious

Several indicators suggest malicious activity:

Newly created service-like account
Rapid privilege assignment
Remote access permissions granted
Correlation with RDP logon activity
Persistence-oriented behavior

Threat actors frequently create accounts with names such as:

svc_backup
sys_restore
helpdesk_admin
winupdate

to blend into enterprise environments.

Skills Demonstrated
Windows Event Log Analysis
Authentication Investigation
User Management Event Correlation
Threat Hunting
Detection of Persistence Mechanisms
Logon ID Correlation
Privilege Escalation Analysis

Tools Used:
Windows Event Viewer
Microsoft Windows Security Logs
TryHackMe

Relevant Windows Event IDs:
Event ID	Description
4624	Successful Logon
4720	User Account Created
4732	User Added to Security Group
Conclusion

The investigation identified a malicious persistence mechanism established shortly after an RDP compromise. The attacker created a stealthy backdoor account (svc_sysrestore) and added it to privileged groups to maintain remote administrative access within the environment.
   ↓
Logon Type 10 → RDP session established
   ↓
Logon ID 0x183C36D → Session tracking identifier
Conclusion

The system was successfully compromised via brute force attack, leading to administrative RDP access. The Logon ID enables full post-compromise forensic tracking.
