# Week 06 - Vulnerability Detection and Authentication Failures

## 1. Objective

Verify that Wazuh detects software vulnerabilities and identifies authentication failures on monitored endpoints.

## 2. Lab Environment

| Property | Details |
|---|---|
| Cloud Provider | AWS EC2 |
| Region | Mumbai (`ap-south-1`) |
| Wazuh Version | `4.14.7` |
| Manager Private IP | `10.0.1.80` |
| Test Endpoint | `agent-linux-1` |
| Endpoint IP | `10.0.1.237` |
| Operating System | Ubuntu 24.04.5 LTS |

## 3. Vulnerability Detection

### Procedure
1. Checked the Wazuh manager and indexer services.
2. Reviewed the vulnerability-detection configuration.
3. Checked agent connectivity and Syscollector package inventory.
4. Opened the Vulnerability Detection dashboard.
5. Filtered findings by endpoint and inspected the results.

### Results

| Property | Recorded Result |
|---|---|
| Vulnerability Detection | Enabled |
| Agent Software Inventory | Available |
| Findings Displayed | Yes |
| Endpoint | `agent-linux-1` |
| CVE | `CVE-2026-54411` |
| Affected Package | `libpam-runtime` |
| Installed Version | `1.5.3-5ubuntu5.5` |
| Severity | Medium |
| Finding Status | Active / Evaluated |

### Explanation

Wazuh Syscollector collects software and package inventory from monitored endpoints. Vulnerability Detection uses this inventory to identify packages associated with known vulnerabilities and display corresponding findings.

**Assessment:** The recorded results demonstrate that vulnerability findings were available for `agent-linux-1`. The CVE identifier, affected package, version and severity should match the captured dashboard evidence.

## 4. Authentication-Failure Detection

### Procedure
1. Verified the SSH access restrictions for the test endpoint.
2. Performed a small number of controlled failed SSH login attempts.
3. Checked the endpoint's authentication logs.
4. Searched the Wazuh dashboard for matching events.
5. Recorded the alert details.

### Results

| Property | Recorded Result |
|---|---|
| Failed Login Attempts | Performed |
| Matching Local Log Entry | Found |
| Event Visible in Wazuh | Yes |
| Agent Name / ID | `agent-linux-1` / `002` |
| Event Timestamp | `Oct 12, 2026 @ 04:41:32.785` |
| Source IP | `13.207.188.148` |
| Rule ID | `5710` |
| Rule Level | `5` |
| Brute-Force Alert | Not triggered |

### Explanation

The Wazuh agent forwards configured authentication logs to the manager, where decoders and rules analyse the events.

The recorded Rule `5710` event identifies an SSH login attempt using a non-existent user. The individual failed-login event was detected, but the limited test attempts did not trigger a higher-level brute-force alert.

**Assessment:** The test demonstrated detection of individual SSH authentication failures. It did not demonstrate brute-force threshold detection.

## 5. Evidence

The following screenshots were recorded:

- `W6D1_1_Vulnerability_Detection_Status.png`
- `W6D1_2_Linux-1_Endpoint_Software_Inventory.png`
- `W6D1_3.1_Linux-1_Vulnerability_Findings.png`
- `W6D1_3.2_Linux-1_Vulnerability_Details.png`
- `W6D1_4_Local_Auth_Log.png`
- `W6D1_5_SSH_Failed_Login_Event.png`
- `W6D1_6_Authentication_Alert_Details.png`

## 6. Conclusion

Week 6 focused on vulnerability detection and authentication failure monitoring.

The recorded evidence indicates that Wazuh displayed vulnerability findings for `agent-linux-1` and detected individual failed SSH login attempts under Rule `5710`.

A brute-force alert was not triggered during the limited authentication-failure test. Therefore, the results demonstrate individual authentication-failure detection, not successful verification of brute-force threshold detection.

Overall the recorded results support the two tested monitoring capabilities, subject to verification of the evidence and environment details.