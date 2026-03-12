# ELK Log Analysis

## Description

This project demonstrates basic log analysis using the ELK stack.  
The investigation was performed using Kibana to search, filter, and analyze log events.

## Tools Used

- Elasticsearch
- Logstash
- Kibana
- Log analysis techniques

## Investigation Screenshots

### Viewing VPN Logs

![VPN Logs](images/elk_all_vpn_logs.png)

### Filtering Login Events

![Login Events](images/elk_vpn_login_events.png)

### Investigating Source IP Addresses

![Source IP Analysis](images/elk_top_source_ips.png)

### Investigating VPN Users

![User Analysis](images/elk_vpn_users.png)

### Investigating a Specific User

The query `UserName:"James"` was used to identify VPN login events associated with a specific user.

![User Query](images/elk_user_query.png)

### Investigating a Specific IP Address

The query `Source_ip:"157.109.0.102"` was used to investigate VPN activity originating from a specific IP address.

![IP Query](images/elk_ip_query.png)

## Findings

- VPN login events were successfully identified using the query `action:"built"`.
- A total number of login events were observed within the selected time range.
- Source IP addresses were analyzed to determine where VPN connections originated.
- User activity analysis showed that specific users generated multiple VPN login events.

This investigation demonstrates how ELK can be used to filter, search, and analyze log data in a security monitoring environment.