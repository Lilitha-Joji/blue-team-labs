# VPN Log Analysis (SOC Investigation)

## Overview

This project demonstrates how VPN authentication logs were analyzed using Splunk to detect user login activity and investigate connection patterns.

The logs contain VPN session events including:

- Session creation (built)
- Session termination (teardown)

## Log Fields

The following fields were analyzed:

UserName  
Source_ip  
Source_Country  
EventTime  
action  
protocol  
port  
source_state  

## Investigation Objective

Identify how many times users logged into the VPN service and analyze connection behavior.

## Key Concept

action = built → VPN login  
action = teardown → VPN logout

## Tools Used

- Splunk
- JSON log analysis
- SOC investigation techniques
## Investigation Screenshots

## Uploading the VPN Logs

![Upload Logs](images/upload_logs.png)

## Viewing All VPN Logs

![All Logs](images/all_logs_view.png)

## Filtering VPN Login Events

![Login Events](images/vpn_login_filter.png)

## Counting Logins Per User

![User Login Count](images/login_count_users.png)
## Findings

The analysis revealed that several users established VPN sessions.
Login activity was identified using the `action=built` event.

Splunk queries were used to count login events per user and analyze
connection activity across the dataset.