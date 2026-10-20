# Week 05 - Log Ingestion and File Integrity Monitoring

## 1. Objective

The objective of Week 5 was to verify that endpoint logs could be collected and reviewed centrally through Wazuh and to test File Integrity Monitoring (FIM) by modifying a file in a dedicated test directory.

The main objectives were to:

- Verify that the Ubuntu endpoint was connected to the Wazuh manager.
- Generate a normal administrative event on the endpoint.
- Confirm that the corresponding event appeared in the Wazuh dashboard.
- Configure FIM to monitor a dedicated test directory.
- Modify a monitored file and verify that Wazuh detected the change.
- Capture screenshots documenting the test procedures and results.

---

## 2. Lab Environment

| Property | Configuration |
|---|---|
| Cloud Platform | Amazon Web Services (AWS) EC2 |
| AWS Region | Mumbai - `ap-south-1` |
| Wazuh Manager Private IP | `10.0.1.80` |
| Wazuh Version | `4.14.7` |
| Test Endpoint | `agent-linux-1` |
| Endpoint Private IP | `10.0.1.237` |
| Endpoint Operating System | Ubuntu |

The Ubuntu endpoint was used for the log ingestion and File Integrity Monitoring tests.

---

## 3. Log Ingestion Test

### 3.1 Purpose

The purpose of this test was to verify that an administrative event generated on the Ubuntu endpoint could be recorded locally and subsequently viewed in the Wazuh dashboard.

### 3.2 Test Procedure

The following steps were recorded during the test:

1. Checked that the Wazuh agent service was running.
2. Reviewed recent authentication related logs on the Ubuntu endpoint.
3. Generated an administrative event by executing:

   `sudo whoami`

4. Searched the Wazuh dashboard for the corresponding event.
5. Reviewed the event details, including its timestamp, agent name, rule ID, and description.

### 3.3 Test Results

| Property | Recorded Result |
|---|---|
| Local log entry found | Yes |
| Corresponding event visible in Wazuh | Yes |
| Event Timestamp | `Oct 11, 2026 @ 02:58:46.883` |
| Agent Name | `agent-linux-1` |
| Rule ID | `5402` |
| Rule Description | `Successful sudo to ROOT executed` |

### 3.4 Technical Explanation

Log ingestion allows endpoint activity to be collected and reviewed centrally.

The Wazuh agent collects configured log data and forwards it to the Wazuh manager. The manager processes the incoming events using its analysis components, including decoders and rules.

When an event matches a detection rule, Wazuh can generate an alert that can be reviewed in the dashboard.

In this test, the recorded result was a successful `sudo` event associated with rule ID `5402`.

### 3.5 Result

**Recorded outcome: Successful.**

---

## 4. File Integrity Monitoring (FIM) Test

### 4.1 Purpose

The purpose of this test was to verify that Wazuh could detect a change to a file inside a configured, monitored directory.

### 4.2 Test Configuration

| Property | Configuration |
|---|---|
| Monitored Endpoint | `agent-linux-1` |
| Monitored Directory | `/home/ubuntu/socwatch-fim-test` |
| Test File | `test-file.txt` |
| Monitoring Mode | Real time |
| Agent Configuration File | `/var/ossec/etc/ossec.conf` |

The dedicated test directory was used to demonstrate file change detection without intentionally modifying an important system file.

### 4.3 Test Procedure

The following steps were recorded during the test:

1. Created the test directory and an initial test file.
2. Added the test directory to the existing FIM configuration.
3. Restarted the Wazuh agent.
4. Checked the agent service status after the configuration change.
5. Modified `test-file.txt`.
6. Searched the Wazuh dashboard for the corresponding file integrity event.
7. Reviewed the event description and rule ID.

### 4.4 Test Results

| Property | Recorded Result |
|---|---|
| Test File Modified | Yes |
| FIM Event Visible in Wazuh | Yes |
| Event Timestamp | `Oct 11, 2026 @ 05:21:49.108` |
| Agent Name | `agent-linux-1` |
| Rule ID | `550` |
| Event Description | `Integrity checksum changed.` |

### 4.5 Technical Explanation

File Integrity Monitoring helps identify changes to files and directories that are configured for monitoring.

Wazuh records information about monitored files, including cryptographic checksums and other file attributes. When a monitored file changes, Wazuh can compare the updated attributes with previously recorded information and generate an event describing the change.

For this test:

- The monitored directory was `/home/ubuntu/socwatch-fim-test`.
- The test file was `test-file.txt`.
- The file was modified after FIM was configured.
- The recorded dashboard event reported that the integrity checksum had changed.
- The recorded rule ID was `550`.

The observed event supports the conclusion that Wazuh detected the tested file modification.

### 4.6 Result

**Recorded outcome: Successful.**

---

## 5. Evidence Captured

The following screenshot filenames were recorded in the original project notes.

| Screenshot Filename | Evidence Purpose |
|---|---|
| `W5D1_1_Three_Agents_Active.png` | Documents the status of the three enrolled agents |
| `W5D1_2_Linux_Log_Ingestion.png` | Supports the Ubuntu log ingestion test |
| `W5D1_3_Linux_Log_Ingestion_Dashboard.png` | Shows the corresponding event in the Wazuh dashboard |
| `W5D1_4_Windows_Log_Ingestion.png` | Documents the Windows log ingestion activity |
| `W5D1_5_FIM_Test_File.png` | Shows the FIM test file and its modification |
| `W5D1_6_FIM_Config.png` | Documents the FIM configuration |
| `W5D1_7_FIM_Alert.png` | Shows the file-integrity event in the Wazuh dashboard |

### Evidence Verification Checklist

- [✓] Confirm that all seven screenshot files exist.
- [✓] Confirm that the screenshots are readable.
- [✓] Confirm that the log ingestion screenshot supports the recorded rule ID and event description.
- [✓] Confirm that the FIM configuration screenshot shows the intended monitored directory and real-time setting.
- [✓] Confirm that the FIM alert screenshot supports the recorded event description and rule ID.
- [✓] Confirm that the screenshots do not expose passwords, access keys, or other credentials.
- [✓] Ensure the screenshots are stored in the appropriate project evidence folder.

---

## 6. Issues and Troubleshooting

Record any issues encountered during the log ingestion or FIM tests.

| Issue | Investigation | Resolution | Final Status |
|---|---|---|---|
| No specific issue recorded in the supplied notes | Not documented | Not documented | Confirm whether troubleshooting occurred |

If no issues occurred, this section can state that no issues were recorded during testing.

If troubleshooting was required, document:

- The symptom or error message.
- The affected endpoint or service.
- The checks performed.
- The corrective action.
- The verification performed after the correction.

Do not add troubleshooting steps that were not actually performed.

---

## 7. Security Considerations

The following considerations apply to the documented tests:

- Use a dedicated test directory for FIM demonstrations.
- Avoid modifying important operating-system files solely to generate test alerts.
- Keep administrator credentials and generated passwords out of the repository.
- Verify that the Wazuh manager and endpoints communicate through the intended network configuration.
- Retain screenshots that demonstrate the actual test results.

The log ingestion test used a normal administrative command, while the FIM test used a dedicated file to demonstrate change detection.

---

## 8. Week 05 Summary

Week 5 focused on validating two important Wazuh monitoring capabilities: log ingestion and File Integrity Monitoring.

### Log Ingestion

The recorded results indicate that an administrative event generated on `agent-linux-1` was found locally and was also visible in the Wazuh dashboard.

The event was associated with rule ID `5402`, described as `Successful sudo to ROOT executed`.

### File Integrity Monitoring

The recorded results indicate that modifying `test-file.txt` in the configured test directory produced a corresponding event in the Wazuh dashboard.

The event description was `Integrity checksum changed.`, with rule ID `550`.

## 9. Next Steps

The next stage of the project should build on the existing log ingestion and FIM tests.

1. Verify that the Linux and Windows agents remain connected to the intended Wazuh manager.
2. Test vulnerability detection and review the findings reported by Wazuh.
3. Test authentication failure detection using an authorised lab procedure.
4. Capture screenshots showing the relevant alerts and event details.
5. Document the test procedure, actual result, and any limitations.
6. Update the final report and evidence index with references to the completed tests.