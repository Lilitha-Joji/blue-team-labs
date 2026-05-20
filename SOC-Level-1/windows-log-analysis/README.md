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

## Failed Login Attempts

![Failed Login](screenshots/failed-login.png)

---

## Additional Failed Login Evidence

![Failed Login 2](screenshots/failed-login2.png)

2. Compromised User Account

The attacker successfully gained access to the system using a valid account.

Event ID: 4624
Account: Administrator
Result: Successful authentication after failed attempts

## Initial Access

![Initial Access](screenshots/initial-access.png)

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
   ↓
Logon Type 10 → RDP session established
   ↓
Logon ID 0x183C36D → Session tracking identifier
Conclusion

The system was successfully compromised via brute force attack, leading to administrative RDP access. The Logon ID enables full post-compromise forensic tracking.
