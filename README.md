# soc-brute-force-investigation
SOC investigation of suspicious authentication activity involving repeated failed logins followed by a successful authentication. Includes log analysis, MITRE ATT&amp;CK mapping, incident documentation, and response recommendations.

## Project Overview

This project demonstrates a simulated Tier 1 SOC investigation of suspicious authentication activity using synthetic log data.

During the investigation, I analyzed authentication logs to identify unusual login behavior, established a timeline of events, compared suspicious activity with previously observed authentication activity, and documented my findings in an incident report.

The investigation identified 18 failed authentication attempts against a single user account from an unusual source IP address, followed by a successful authentication from the same IP.

The observed behavior was mapped to MITRE ATT&CK T1110 – Brute Force.

> **Note:** All users, IP addresses, authentication events, and log data used in this project are synthetic and were created solely for cybersecurity training and portfolio purposes.

## Investigation Objectives

The objectives of this investigation were to:

- Identify suspicious authentication patterns within the provided log data.
- Determine the affected user account and source IP address.
- Establish a timeline of suspicious authentication activity.
- Compare the suspicious activity with previously observed authentication behavior.
- Determine whether a successful authentication occurred following the failed attempts.
- Map the observed behavior to the MITRE ATT&CK framework.
- Recommend appropriate containment and investigation actions.
- Document the investigation in a professional incident report.

  ## Skills Demonstrated

- Security log analysis
- Authentication event analysis
- Incident investigation
- Timeline development
- Identification of suspicious login patterns
- Evidence-based security analysis
- MITRE ATT&CK mapping
- Incident documentation
- Incident response recommendations
- Distinguishing confirmed evidence from analytical assumptions

## Investigation & Findings

### Initial Observation

While reviewing the authentication logs, I identified repeated failed authentication attempts involving the `jlee` account.

Further analysis showed that 18 failed authentication attempts originated from the same source IP address:

`185.77.12.44`

The failed attempts occurred between **9:55:00 AM and 10:01:14 AM on September 18, 2026**.

### Authentication Timeline

| Time | Event | User | Source IP | Result |
|---|---|---|---|---|
| 9:55:00 AM | First suspicious authentication attempt | jlee | 185.77.12.44 | Failed |
| 9:55:00 AM–10:01:14 AM | 18 authentication attempts observed | jlee | 185.77.12.44 | Failed |
| 10:01:14 AM | Final failed authentication attempt | jlee | 185.77.12.44 | Failed |
| 10:02:10 AM | Authentication attempt | jlee | 185.77.12.44 | Successful |

The successful authentication occurred **56 seconds after the final failed attempt**.

### Baseline Comparison

Earlier successful authentication activity for the `jlee` account originated from `10.10.20.15`.

The suspicious authentication sequence originated from `185.77.12.44`, which differed from the source IP previously associated with successful `jlee` authentication activity.

The combination of repeated authentication failures, the change in source IP, and the subsequent successful authentication made the activity worthy of further investigation.

### Analysis

Based on the available evidence, the authentication activity is consistent with possible brute-force activity. The `jlee` account experienced 18 failed authentication attempts within a short time frame, all originating from `185.77.12.44`.

Following the failed attempts, a successful authentication from the same source IP occurred at 10:02:10 AM, 56 seconds after the final failure.

Although the pattern is suspicious, the authentication logs alone do not confirm that the account was compromised or that the successful authentication was unauthorized.

Additional investigation would be required to determine whether the account owner recognized the login and what activity occurred following the successful authentication.

## MITRE ATT&CK Mapping

**Technique:** Brute Force  
**Technique ID:** T1110

The observed authentication behavior is consistent with potential brute-force activity because multiple failed authentication attempts against the same account were followed by a successful authentication from the same source IP.

The available evidence supports mapping the observed behavior to MITRE ATT&CK T1110; however, the authentication logs alone do not confirm that a successful brute-force attack occurred.

## Recommended Response

Based on the findings, I would recommend:

1. Temporarily disable the `jlee` account while the suspicious authentication activity is investigated.
2. Initiate a password reset to invalidate potentially compromised credentials.
3. Verify with the account owner whether the successful authentication from `185.77.12.44` was authorized.
4. Review subsequent account and system activity for evidence of unauthorized access.
5. Preserve relevant authentication and system logs for further investigation.
6. If MFA is not already enabled, require multifactor authentication to strengthen account security.

## Repository Structure

```text
soc-brute-force-investigation/
├── README.md
├── analysis/
│   └── investigation-notes.md
├── logs/
│   └── auth.log
└── report/
    └── incident-report.pdf
