# 📂 Investigation Data

This directory represents the data sources used during the **CEO Account Takeover Investigation**.

## Data Sources

The investigation analyzed simulated Microsoft cloud security telemetry representing activity within the fictional **Cloudora** environment.

The primary datasets consisted of:

- Microsoft 365 sign-in activity
- Authentication success and failure events
- Source IP address and geolocation information
- Application access activity
- Device and browser information
- Security-information / Authenticator registration events
- Mailbox and inbox-rule audit activity

## Data Processing

The datasets were ingested into **Azure Data Explorer** and analyzed using **Kusto Query Language (KQL)**.

The investigation correlated sign-in and audit telemetry to reconstruct the attack timeline, identify persistence activity, determine the affected account, evaluate the broader blast radius, and develop reusable detection logic.

## Key Investigation Fields

Important fields used during analysis included:

| Field | Purpose |
|---|---|
| `TimeGenerated` | Event timestamp and timeline reconstruction |
| `UserPrincipalName` | Identification of targeted user accounts |
| `IPAddress` | Source infrastructure correlation |
| `City` | Geographic analysis |
| `Country` | Geographic analysis |
| `AppDisplayName` | Identification of accessed cloud services |
| `DeviceOS` | Device analysis |
| `Browser` | Client/browser analysis |
| `ResultType` | Authentication success/failure analysis |
| `ActivityDisplayName` | Audit-event identification |
| `InitiatedBy` | Identification of the actor initiating an audit event |
| `TargetUser` | Identification of the affected account |
| `Details` | Additional event context |

## Data Handling

The raw datasets are not included in this public repository.

This repository instead contains:

- KQL investigation queries
- Detection-engineering rules
- Screenshots of relevant query results
- Indicators of compromise
- MITRE ATT&CK mappings
- Reconstructed incident timeline
- Final incident report

This approach preserves the analytical methodology and supporting evidence without publishing the underlying raw telemetry.

## Disclaimer

All users, organizations, IP addresses, events, and security telemetry used in this project are part of a **simulated cybersecurity investigation environment** created for educational and portfolio purposes.
