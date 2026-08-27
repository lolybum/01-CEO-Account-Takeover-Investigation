# MITRE ATT&CK Mapping
## CEO Account Takeover Investigation

### Incident Summary

The investigation identified suspicious authentication activity originating from Lagos, Nigeria, using IP address `102.89.44.17`.

The source IP targeted multiple Cloudora user accounts. Successful authentication was confirmed for `daniel.reeve@cloudora.io`.

Following successful account access, the threat actor registered a new authenticator device and created a suspicious inbox rule.

---

## T1078 - Valid Accounts

**Tactic:** Initial Access / Persistence / Privilege Escalation / Defense Evasion

### Evidence

Successful authentication to Daniel Reeve's account occurred from suspicious IP:

`102.89.44.17`

Successful access included:

- Microsoft 365
- Outlook Web
- Azure Portal

The first confirmed successful authentication occurred at:

`2026-08-10 03:12:05 UTC`

### Analysis

The attacker successfully authenticated using Daniel Reeve's legitimate cloud account credentials.

This activity is consistent with MITRE ATT&CK technique **T1078 - Valid Accounts**.

---

## T1098 - Account Manipulation

**Tactic:** Persistence

### Evidence

At:

`2026-08-10 03:18:44 UTC`

the following audit activity occurred:

**Activity:** User registered security info

**Source IP:** `102.89.44.17`

**Result:** Success

**Details:** Authenticator app added: device `Pixel 6`

### Analysis

The attacker registered an additional authentication mechanism after gaining access to the compromised account.

This could allow continued account access even if the original password were changed.

This activity is consistent with **T1098 - Account Manipulation**.

---



**Tactic:** Collection

### Evidence

At:

`2026-08-10 03:14:30 UTC`

the attacker successfully accessed Outlook Web.

At:

`2026-08-10 03:31:09 UTC`

a new inbox rule was created from the suspicious IP.

The rule was:

`RSS Subscriptions`

The rule matched messages:

- from `finance@cloudora.io`
- containing the word `invoice`

Matching messages were configured to:

- move to RSS Feeds
- mark as read

### Analysis

The inbox rule appears designed to conceal finance-related messages from the account owner.

The Outlook access and mailbox-rule manipulation are relevant to email-focused post-compromise activity.

The evidence confirms post-compromised mailbox manipulation through creation of a suspicious inbox rule. However, the available telemetry does not confirm that email content was collected or exfiltrated; therefore no email collection is asserted.
---

## Attack Progression

1. Multiple Cloudora accounts were targeted from `102.89.44.17`.
2. Daniel Reeve's account experienced failed authentication attempts.
3. Successful Microsoft 365 authentication occurred at 03:12:05 UTC.
4. Outlook Web was accessed at 03:14:30 UTC.
5. A new Authenticator device (`Pixel 6`) was registered at 03:18:44 UTC.
6. Azure Portal was accessed at 03:26:02 UTC.
7. A suspicious inbox rule was created at 03:31:09 UTC.

---

## Confirmed Indicators

| Indicator | Value |
|---|---|
| Compromised Account | daniel.reeve@cloudora.io |
| Suspicious IP | 102.89.44.17 |
| Suspicious Location | Lagos, Nigeria |
| Registered Device | Pixel 6 |
| Malicious Inbox Rule | RSS Subscriptions |

---

## MITRE ATT&CK Summary

| Technique | Technique ID | Evidence |
|---|---|---|
| Valid Accounts | T1078 | Successful access using Daniel Reeve's account |
| Account Manipulation | T1098 | New authenticator registered after compromise |
