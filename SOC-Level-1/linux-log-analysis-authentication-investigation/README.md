# Linux Authentication Log Investigation

## Overview

This project demonstrates basic Linux log analysis using authentication logs located in `/var/log/auth.log`.

The objective was to identify:

1. IP addresses responsible for failed SSH login attempts.
2. User account creation events.
3. Privilege escalation and group membership modifications.

## Skills Demonstrated

* Linux log analysis
* Authentication log investigation
* SSH brute-force detection
* User account monitoring
* Privilege escalation detection
* Command-line log filtering using grep

## Investigation 1: Failed SSH Logins

### Objective

Identify IP addresses responsible for failed SSH authentication attempts.

### Command Used

```bash
cat /var/log/auth.log | grep -E "Failed"
```

### Findings

Multiple failed SSH login attempts were identified.

Suspicious Source IP:

```text
10.14.94.82
```

This IP attempted authentication against multiple user accounts, which may indicate password spraying or brute-force activity.

## Investigation 2: User Creation and Privilege Escalation

### Objective

Identify newly created users and determine whether they were granted administrative privileges.

### Command Used

```bash
cat /var/log/auth.log | grep -E '(passwd|useradd|usermod|userdel)\['
```

### Findings

A user named:

```text
xerves
```

was created and subsequently added to the `sudo` group.

Relevant indicators:

* User creation event (`useradd`)
* Group modification event (`usermod`)
* Administrative privilege assignment (`sudo` group)

This activity should be reviewed during incident response because attackers often create privileged accounts to maintain persistence.

## Key Takeaways

Linux authentication logs provide valuable visibility into:

* User logins
* Failed authentication attempts
* Account creation
* Privilege escalation
* Administrative activity

These logs are often one of the first sources reviewed during Linux incident investigations.
