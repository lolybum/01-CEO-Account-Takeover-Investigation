# Security Incident Report
## CEO Account Takeover Investigation — Cloudora

**Incident ID:** CLD-0001  
**Severity:** P1 — Critical  
**Incident Type:** Executive Account Takeover  
**Affected Account:** daniel.reeve@cloudora.io  
**Organization:** Cloudora  
**Investigation Platform:** Azure Data Explorer / KQL  
**Status:** Confirmed Compromise  

---

# 1. Executive Summary

Cloudora identified suspicious authentication activity involving the account of CEO Daniel Reeve.

Investigation of authentication and audit telemetry confirmed that the account was accessed from the suspicious IP address `102.89.44.17`, associated in the provided sign-in telemetry with Lagos, Nigeria.

The activity progressed from failed authentication attempts to successful access to Microsoft 365, Outlook Web, and Azure Portal.

Following successful authentication, security information was registered for the compromised account using an Authenticator application associated with a `Pixel 6` device.

A suspicious inbox rule named `RSS Subscriptions` was subsequently created. The rule targeted messages from `finance@cloudora.io` or messages containing `invoice`, moved matching messages to RSS Feeds, and marked them as read.

The investigation therefore assesses the incident as a **confirmed account compromise with post-compromise persistence and mailbox manipulation**.

Available telemetry does not independently establish data exfiltration.

---

# 2. Incident Scope

The investigation examined activity associated with:

**Primary affected account**

`daniel.reeve@cloudora.io`

**Suspicious source IP**

`102.89.44.17`

The suspicious IP was observed attempting authentication against multiple Cloudora accounts.

Most accounts showed unsuccessful authentication attempts.

Daniel Reeve's account was confirmed to have successful authentication from the suspicious IP.

This indicates broader credential-targeting activity with confirmed compromise of the CEO account.

---

# 3. Investigation Timeline

| Time (UTC) | Event | Result | Assessment |
|---|---|---|---|
| 2026-08-10 00:35:48 | Microsoft 365 authentication attempt | Failed | Initial observed failed attempt |
| 2026-08-10 03:09:12 | Microsoft 365 authentication attempt | Failed | Continued authentication attempts |
| 2026-08-10 03:10:41 | Microsoft 365 authentication attempt | Failed | Continued authentication attempts |
| 2026-08-10 03:12:05 | Microsoft 365 authentication | Success | First confirmed successful access |
| 2026-08-10 03:14:30 | Outlook Web authentication | Success | Mailbox access |
| 2026-08-10 03:18:44 | Security information registered | Success | New Authenticator registration |
| 2026-08-10 03:26:02 | Azure Portal authentication | Success | Cloud management access |
| 2026-08-10 03:31:09 | New inbox rule created | Success | Suspicious mailbox manipulation |

---

# 4. Authentication Analysis

Authentication telemetry showed repeated activity originating from:

`102.89.44.17`

The source was identified in the dataset as:

**Lagos, Nigeria**

Three successful authentication events were confirmed:

- Microsoft 365 — 03:12:05 UTC
- Outlook Web — 03:14:30 UTC
- Azure Portal — 03:26:02 UTC

These events occurred after unsuccessful authentication attempts from the same suspicious source.

The sequence is consistent with successful account takeover followed by access to multiple Microsoft cloud services.

---

# 5. Persistence Analysis

At `03:18:44 UTC`, approximately six minutes after the first confirmed successful authentication, audit telemetry recorded:

**Activity:** User registered security info  
**Account:** daniel.reeve@cloudora.io  
**Source IP:** 102.89.44.17  
**Result:** Success  
**Details:** Authenticator app added — device `Pixel 6`

The registration of additional authentication information following suspicious account access represents a significant persistence indicator.

An attacker-controlled authentication method could potentially permit continued access even after the original password was changed.

---

# 6. Mailbox Manipulation

At `03:31:09 UTC`, the following audit activity was recorded:

**Activity:** New inbox rule created  
**Account:** daniel.reeve@cloudora.io  
**Source IP:** 102.89.44.17  
**Result:** Success  
**Rule:** RSS Subscriptions

The rule targeted messages:

- originating from `finance@cloudora.io`
- containing the term `invoice`

Matching messages were configured to:

- move to RSS Feeds
- mark as read

The behavior could conceal finance-related correspondence from the legitimate account owner.

This represents suspicious post-compromise mailbox manipulation.

---

# 7. Indicators of Compromise

| IOC Type | Indicator | Confidence |
|---|---|---|
| IP Address | 102.89.44.17 | High |
| Location in telemetry | Lagos, Nigeria | High |
| Compromised Account | daniel.reeve@cloudora.io | High |
| Registered Device | Pixel 6 | High |
| Suspicious Inbox Rule | RSS Subscriptions | High |

---

# 8. MITRE ATT&CK Mapping

| Technique | ID | Evidence |
|---|---|---|
| Valid Accounts | T1078 | Successful authentication using the compromised executive account |
| Account Manipulation | T1098 | Additional Authenticator security information registered after compromise |
| Email Collection / Mailbox Activity | T1114 | Outlook Web access and suspicious mailbox-rule activity |

The ATT&CK mappings describe observed or strongly supported behavior. The investigation does not claim that email contents were successfully exfiltrated.

---

# 9. Impact Assessment

The affected account belongs to the CEO, increasing the potential business impact of the compromise.

Observed attacker activity provided access to:

- Microsoft 365
- Outlook Web
- Azure Portal

The creation of a finance-related inbox rule introduces additional risk involving sensitive business communications, financial transactions, invoice fraud, or business email compromise.

However, the available telemetry does not independently prove that financial fraud or data exfiltration occurred.

**Overall Incident Severity: Critical / P1**

---

# 10. Containment and Remediation Recommendations

Immediate containment actions should include:

1. Reset the compromised account password.
2. Revoke all active sessions and authentication tokens.
3. Remove the unauthorized Authenticator registration.
4. Remove the suspicious `RSS Subscriptions` inbox rule.
5. Investigate or block `102.89.44.17` across relevant security controls.
6. Review mailbox activity for access to sensitive communications.
7. Review Azure Portal activity for unauthorized administrative changes.
8. Investigate every account targeted by the suspicious IP.
9. Review authentication telemetry for related infrastructure and anomalous locations.
10. Increase monitoring of executive and privileged accounts.

Longer-term security improvements should include:

- phishing-resistant MFA for executive and privileged accounts
- alerts for MFA/security-information registration
- alerts for suspicious inbox-rule creation
- impossible-travel and anomalous-location monitoring
- stronger conditional-access policies
- enhanced monitoring for executive accounts

---

# 11. Investigation Conclusion

The investigation confirms that Daniel Reeve's Cloudora account was compromised.

The evidence demonstrates a clear progression from unsuccessful authentication attempts to successful cloud authentication, Outlook access, additional authentication-method registration, Azure Portal access, and suspicious inbox-rule creation.

The source IP `102.89.44.17` also attempted authentication against multiple Cloudora accounts, indicating broader credential-targeting activity.

The strongest evidence of post-compromise persistence was the registration of an Authenticator application associated with a `Pixel 6`.

The suspicious inbox rule further demonstrates post-compromise manipulation of the CEO's mailbox.

Based on the available evidence, the incident should be treated as a **P1 executive account compromise requiring immediate containment, credential reset, session revocation, persistence removal, mailbox review, and continued monitoring**.

No conclusion of confirmed data exfiltration should be made without additional supporting telemetry.

---

# 12. Investigation Artifacts

Supporting project artifacts include:

- Baseline sign-in analysis
- CEO-specific sign-in investigation
- IP and geographic analysis
- Persistence investigation
- Scope analysis
- Unified incident timeline
- Indicators of Compromise documentation
- MITRE ATT&CK mapping
- Azure Data Explorer evidence screenshots
