# Indicators of Compromise (IOC)
## CEO Account Takeover Investigation

### Incident

**Organization:** Cloudora  
**Affected User:** daniel.reeve@cloudora.io  
**Incident Type:** Cloud Account Takeover  
**Severity:** Critical / P1  
**Investigation Date:** August 2026

---

## Confirmed Indicators

| IOC Type | Indicator | Context | Confidence |
|---|---|---|---|
| IP Address | 102.89.44.17 | Source of successful unauthorized authentication and post-compromise activity | High |
| Location | Lagos, Nigeria | Location associated with suspicious authentication activity | High |
| User Account | daniel.reeve@cloudora.io | Confirmed compromised executive account | High |
| Device | Pixel 6 | Device identified when new Authenticator security information was registered | High |
| Inbox Rule | RSS Subscriptions | Suspicious inbox rule created after account compromise | High |

---

## Authentication Indicators

The suspicious IP address `102.89.44.17` generated both failed and successful authentication attempts against Daniel Reeve's account.

### Confirmed Successful Access

| Time (UTC) | Application | Source IP | Location | Result |
|---|---|---|---|---|
| 2026-08-10 03:12:05 | Microsoft 365 | 102.89.44.17 | Lagos, Nigeria | Success |
| 2026-08-10 03:14:30 | Outlook Web | 102.89.44.17 | Lagos, Nigeria | Success |
| 2026-08-10 03:26:02 | Azure Portal | 102.89.44.17 | Lagos, Nigeria | Success |

The first confirmed successful authentication occurred at:

`2026-08-10 03:12:05 UTC`

---

## Persistence Indicator

At:

`2026-08-10 03:18:44 UTC`

the compromised account registered new security information.

**Activity:** User registered security info  
**Source IP:** 102.89.44.17  
**Result:** Success  
**Details:** Authenticator app added: device `Pixel 6`

This activity occurred approximately six minutes after the first confirmed successful authentication.

The registration of an additional authentication mechanism is considered a high-confidence persistence indicator.

---

## Mailbox Indicator

At:

`2026-08-10 03:31:09 UTC`

a new inbox rule was created.

**Rule Name:** RSS Subscriptions  
**Source IP:** 102.89.44.17  
**Result:** Success

The rule targeted messages:

- from `finance@cloudora.io`
- containing `invoice`

Matching messages were configured to:

- move to RSS Feeds
- mark as read

This rule could conceal finance-related messages from the legitimate account owner and represents suspicious post-compromise mailbox manipulation.

---

## Scope Analysis

The suspicious IP address was observed attempting authentication against multiple Cloudora accounts.

Most targeted accounts showed failed authentication attempts.

Daniel Reeve's account was confirmed to have successful authentication from the suspicious IP during the investigated activity.

This indicates broader credential-targeting activity with confirmed compromise of the CEO account.

---

## Recommended IOC Response Actions

1. Block or investigate `102.89.44.17` across relevant identity, cloud, proxy, firewall, and security monitoring systems.
2. Reset credentials for the compromised account.
3. Revoke active sessions and authentication tokens.
4. Remove the unauthorized Authenticator registration associated with the Pixel 6.
5. Remove the suspicious `RSS Subscriptions` inbox rule.
6. Review mailbox activity for access to sensitive financial or enterprise communications.
7. Review all accounts targeted by the suspicious IP for additional compromise indicators.
8. Review authentication logs for related IP addresses and anomalous geographic activity.
9. Require phishing-resistant MFA for privileged and executive accounts where feasible.
10. Continue monitoring for recurrence of the identified indicators.

---

## Investigation Assessment

The available evidence supports a high-confidence determination that the CEO account was compromised.

The attacker successfully authenticated from the suspicious Lagos-associated IP, accessed multiple Microsoft cloud services, registered additional authentication information, and created a suspicious mailbox rule.

The evidence confirms unauthorized account access and persistence-related activity. The available logs do not, by themselves, prove data exfiltration.
