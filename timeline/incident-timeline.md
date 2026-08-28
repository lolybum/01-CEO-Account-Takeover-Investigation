# Incident Timeline — CEO Account Takeover

## Incident Overview

This timeline reconstructs the confirmed sequence of authentication and post-compromise activity associated with the compromise of the Cloudora CEO account.

**Compromised Account:** `daniel.reeve@cloudora.io`  
**Suspicious Source IP:** `102.89.44.17`  
**Suspicious Location:** Lagos, Nigeria  
**Incident Severity:** Critical / P1  
**Incident Date:** 2026-08-10  

---

## Chronological Timeline

| Time (UTC) | Event | Result | Analyst Assessment |
|---|---|---|---|
| 00:35:48 | Microsoft 365 authentication attempt | Failed | Early authentication attempt from suspicious source IP |
| 03:09:12 | Microsoft 365 authentication attempt | Failed | Continued attempts against the executive account |
| 03:10:41 | Microsoft 365 authentication attempt | Failed | Repeated authentication failure immediately before successful access |
| 03:12:05 | Microsoft 365 authentication | Success | First confirmed successful authentication from Lagos, Nigeria |
| 03:14:30 | Outlook Web access | Success | Attacker obtained access to the executive mailbox |
| 03:18:44 | Authenticator registration | Success | New authentication method registered using device `Pixel 6` |
| 03:26:02 | Azure Portal access | Success | Compromised account successfully accessed Azure Portal |
| 03:31:09 | Inbox rule creation | Success | Suspicious `RSS Subscriptions` inbox rule created |

---

## Attack Progression

### 1. Authentication Attempts

Multiple failed authentication attempts were observed from `102.89.44.17`.

The failed attempts were followed by a successful Microsoft 365 authentication at **03:12:05 UTC**.

This transition from repeated failures to successful authentication is consistent with account compromise using valid credentials.

### 2. Successful Account Access

Following successful authentication, the account accessed:

- Microsoft 365
- Outlook Web
- Azure Portal

The geographic origin, Lagos, Nigeria, was inconsistent with the account's established London, United Kingdom sign-in baseline.

### 3. Persistence Activity

At **03:18:44 UTC**, a new authentication method was registered.

Audit telemetry identified:

`Authenticator app added: device 'Pixel 6'`

This represents post-compromise account manipulation that could provide continued access to the compromised account.

### 4. Mailbox Manipulation

At **03:31:09 UTC**, a new inbox rule named:

`RSS Subscriptions`

was created.

The rule targeted messages:

- originating from `finance@cloudora.io`
- containing the word `invoice`

Matching messages were configured to:

- move to RSS Feeds
- be marked as read

This behavior is consistent with suspicious post-compromise mailbox manipulation intended to reduce the visibility of finance-related communications.

---

## Scope

Analysis of the suspicious source IP identified authentication activity against multiple Cloudora accounts.

The detection-engineering analysis identified:

- **48 failed authentication attempts**
- **23 distinct targeted accounts**
- **Source IP:** `102.89.44.17`

Available telemetry confirms successful compromise of Daniel Reeve's account. Other accounts observed in the failed-authentication activity require additional investigation before compromise can be asserted.

---

## Confirmed Indicators

| IOC Type | Indicator |
|---|---|
| Compromised Account | `daniel.reeve@cloudora.io` |
| Suspicious IP | `102.89.44.17` |
| Suspicious Location | Lagos, Nigeria |
| Registered Device | `Pixel 6` |
| Suspicious Inbox Rule | `RSS Subscriptions` |

---

## Conclusion

The reconstructed timeline demonstrates progression from failed authentication attempts to successful executive-account access, followed by Outlook Web access, unauthorized authentication-method registration, Azure Portal access, and suspicious mailbox-rule creation.

The sequence provides strong evidence of a successful account takeover followed by post-compromise persistence and mailbox manipulation.

The available telemetry does not independently establish that email contents were successfully collected or exfiltrated.
