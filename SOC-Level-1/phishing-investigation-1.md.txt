# Phishing Investigation 1

## Alert Dashboard

![SOC Alert Dashboard](images/phishing-alert-dashboard.png)

## Scenario
Introduction to Phishing – TryHackMe SOC Simulator

## Alert Summary
An alert was triggered because an inbound email contained external links with suspicious characteristics.

## Alert Details
Data Source: Email  
Timestamp: 03/07/2026 16:56:13  
Subject: Action Required: Finalize Your Onboarding Profile  
Sender: onboarding@hrconnex.thm  
Recipient: j.garcia  

## Investigation Steps

1. Reviewed the email subject line.
2. Checked the sender email address.
3. Identified that the alert was triggered because of external links in the email.
4. Reviewed the context of the message.
5. Compared the time the email was sent and when the alert was triggered.

## Findings

The email appeared to be related to onboarding and profile setup.  
The sender address looked legitimate in the scenario context.  
No malicious indicators were found during the review.

## Conclusion

This alert was classified as a **False Positive** because the email was part of a legitimate onboarding process.

## Skills Demonstrated

Email analysis  
SOC alert triage  
Phishing investigation  
False positive classification