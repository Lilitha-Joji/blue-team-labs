
# Phishing Email Investigation – Home Depot Impersonation

## 1. Executive Summary

This investigation focuses on a phishing email impersonating Home Depot. The analysis was conducted using the email sample `email3.eml` in the TryHackMe environment.

The investigation involved examining the original email, identifying the impersonated organisation, analysing sender information, inspecting raw email headers and extracting relevant indicators of compromise (IOCs).

The objective was to understand the email's characteristics and identify information that could assist with further security investigation.

## 2. Investigation Environment

| Category | Details |
|---|---|
| Platform | TryHackMe |
| Email Sample | email3.eml |
| Email Client | Mozilla Thunderbird |
| Analysis Type | Email Header Analysis |
| Investigation Focus | Phishing and Sender Impersonation |

## 3. Home Depot Impersonation

During the investigation, Home Depot was identified as the reputable organisation being impersonated in the phishing attempt.

Brand impersonation is a common phishing technique in which attackers misuse the identity of a legitimate organisation to make malicious communications appear trustworthy.

### Evidence 1 – Home Depot Impersonation

![Home Depot Impersonation](../evidence/home-depot-impersonation.png)

## 4. Original Email Analysis

The original email was examined using Mozilla Thunderbird to identify the sender and inspect the message presented to the recipient.

The following sender address was identified:

**Sender:** `support@teckbe.com`

The sender address uses the `teckbe.com` domain, while the organisation identified as being impersonated was Home Depot.

This discrepancy is an important observation when assessing the authenticity of the email.

### Evidence 2 – Original Email

![Original Email](../evidence/original-email.png)

## 5. Email Header Analysis

The raw email source was inspected using Thunderbird's Message Source feature.

Viewing the raw message source provides access to technical email headers that are not necessarily visible in the standard inbox view.

One of the important fields identified during this investigation was `X-Originating-IP`.

### 5.1 X-Originating-IP Analysis

The following IP address was identified:

**Original IP Address:**

`103.234.236.83`

**Defanged IP Address:**

`103[.]234[.]236[.]83`

The IP address was extracted from the `X-Originating-IP` header and documented as an indicator for further investigation.

### Evidence 3 – Original IP

![Original IP](../evidence/original-ip.png)

## 6. Authentication-Results Analysis

The raw email source was further inspected to identify the mail server associated with the `Authentication-Results` header.

The identified server was:

`atlas102.free.mail.gq1.yahoo.com`

The Authentication-Results header provides information about email authentication checks performed by a mail system.

This information is useful when investigating email authenticity and the infrastructure involved in message processing.

The specific SPF, DKIM and DMARC outcomes would need to be examined separately before drawing conclusions about authentication.

### Evidence 4 – Authentication Results

![Authentication Results](../evidence/authentication-results.png)

## 7. Indicators of Compromise (IOCs)

The following indicators were extracted during the investigation:

| Indicator Type | Observed Value | Description |
|---|---|---|
| Email Address | support@teckbe.com | Identified sender address |
| Domain | teckbe.com | Sender email domain |
| IP Address | 103[.]234[.]236[.]83 | X-Originating-IP |
| Mail Server | atlas102.free.mail.gq1.yahoo.com | Server identified in Authentication-Results |

These indicators can be used as starting points for further investigation and correlation with other security events.

## 8. Investigation Findings

The investigation established the following findings:

1. Home Depot was identified as the organisation being impersonated.
2. The sender address was identified as `support@teckbe.com`.
3. The sender domain differed from the impersonated organisation.
4. The `X-Originating-IP` header contained `103.234.236.83`.
5. The `Authentication-Results` header identified `atlas102.free.mail.gq1.yahoo.com`.
6. Relevant email information was extracted and documented for further investigation.

## 9. Conclusion

This investigation demonstrated how email analysis and raw message headers can be used to examine a suspected phishing attempt.

By reviewing the original email and inspecting its underlying message source, it was possible to identify the impersonated organisation, extract sender information, identify the originating IP address and examine the Authentication-Results header.

The findings highlight the importance of examining email metadata rather than relying exclusively on the information displayed in an inbox.

Further analysis of email authentication outcomes, sender domain reputation and any embedded URLs would provide additional evidence for assessing the threat.

## 10. Tools and Techniques

- TryHackMe – Phishing investigation lab
- Mozilla Thunderbird – Email inspection and raw message source
- Manual email header analysis
- IOC extraction
- IP address defanging

---

**Project Category:** Blue Team / SOC Investigation  
**Investigation Type:** Phishing Email Analysis  
**Focus Area:** Email Header Forensics

