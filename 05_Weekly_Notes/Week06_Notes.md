# Week 06 — Vulnerability Detection and Authentication Failures

## 1. Objective

The objective of Week 6 was to verify vulnerability detection on a monitored endpoint and demonstrate that Wazuh can detect and display authentication-failure events.

## 2. Lab Environment

* Cloud provider: AWS EC2
* Region: Mumbai (`ap-south-1`)
* Wazuh version: `4.14.7`
* Manager private IP: `10.0.1.80`
* Main test endpoint: `agent-linux-1`
* Endpoint private IP: `65.0.133.4`
* Endpoint OS: Ubuntu 24.04.5 LTS

## 3. Vulnerability Detection

### Procedure

1. Checked the Wazuh manager and indexer services.
2. Checked the manager's vulnerability-detection configuration.
3. Checked the agent service and Syscollector package-inventory settings.
4. Opened the Vulnerability Detection section in the dashboard.
5. Filtered the results by the test endpoint and inspected available findings.

### Results

* Vulnerability detection enabled: Yes
* Agent inventory available: Yes
* Findings displayed: Yes
* Endpoint: agent-linux-1
* CVE ID: CVE-2026-54411
* Affected package and version: libpam-runtime (1.5.3-5ubuntu5.5)
* Severity: Medium
* Finding status: Active / Evaluated

### Explanation

Wazuh utilizes the Syscollector module to continuously gather comprehensive software and package inventories from monitored endpoints. The Vulnerability Detection module then correlates this inventory data against external vulnerability intelligence feeds and CVE databases. When an installed package version matches a known vulnerable version, Wazuh generates a security finding referencing the specific Common Vulnerabilities and Exposures (CVE) identifier.

### Assessment

The vulnerability detection module successfully leveraged Wazuh's Syscollector component to gather a comprehensive software and package inventory from agent-linux-1. By cross-referencing these installed package versions against vulnerability intelligence feeds, the system surfaced active security findings, such as CVE-2026-54411 affecting libpam-runtime version 1.5.3-5ubuntu5.5 with a Medium severity rating. This demonstrates the core capability of continuous posture assessment, allowing security teams to quickly identify and prioritize patch management for vulnerable components across managed cloud endpoints.

## 4. Authentication-Failure Detection

### Procedure

1. Verified that SSH access to the test endpoint was restricted to the current administrator IP.
2. Made a small number of controlled failed SSH login attempts against the lab endpoint.
3. Checked the endpoint authentication log.
4. Searched the Wazuh dashboard for the corresponding event.
5. Recorded the rule details if an alert was generated.

### Results

* Failed login attempted: Yes
* Matching local log entry: Yes
* Matching event visible in Wazuh: Yes
* Agent name and ID: agent-linux-1 / 002
* Event timestamp: Oct 12, 2026 @ 04:41:32.785
* Source IP: 13.207.188.148
* Rule ID: 5710
* Severity: rule.level 5
* Brute force detection triggered: No (only single authentication-failure alerts were generated under Rule 5710; rule conditions for a brute force threshold alert were not met)

### Explanation

Authentication logs capture system access attempts, including detailed metadata such as source IP addresses and target usernames. When the Wazuh agent forwards `/var/log/auth.log` messages to the manager, Wazuh decoders parse the log text into structured fields. The rules engine then correlates these fields against standard rule sets—triggering `Rule 5710` ("sshd: Attempt to login using a non-existent user") upon detecting an invalid user login attempt. Because only a small number of controlled tests were performed, Wazuh recorded individual failed-login events without escalating to a higher-level SSH brute-force alert.

## 5. Evidence

* `W6D1_1_Vulnerability_Detection_Status.png`
* `W6D1_2_Linux-1_Endpoint_Software_Inventory.png`
* `W6D1_3.1_Linux-1_Vulnerability_Findings.png`
* `W6D1_3.2_Linux-1_Vulnerability_Details.png`
* `W6D1_4_Local_Auth_Log.png`
* `W6D1_5_SSH_Failed_Login_Event.png`
* `W6D1_6_Authentication_Alert_Details.png`

## 6. Troubleshooting

No persistent errors or configuration troubleshooting were required.

## 7. Conclusion

During Week 6, the vulnerability detection module was successfully verified, with Wazuh's Syscollector and vulnerability intelligence feeds correctly surfacing active package findings (such as CVE-2026-54411 on `libpam-runtime`) for `agent-linux-1`. Furthermore, controlled failed SSH login attempts were successfully generated from an external IP address, verified locally within `/var/log/auth.log` and successfully detected and displayed in the Wazuh dashboard under Rule 5710 ("sshd: Attempt to login using a non-existent user"). Because only a limited number of test attempts were performed, brute-force alert thresholds were not reached, which aligns with expected rule conditions. Overall all objectives for vulnerability and authentication-failure monitoring were successfully completed and documented.