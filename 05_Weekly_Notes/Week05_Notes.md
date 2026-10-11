# Week 05 — Log Ingestion and File Integrity Monitoring

## 1. Objective

The objective of this stage was to verify that endpoint logs can be monitored centrally through Wazuh and to test File Integrity Monitoring (FIM) by changing a file in a dedicated test directory.

## 2. Lab Environment

* Cloud platform: AWS EC2
* Region: Mumbai (`ap-south-1`)
* Wazuh manager private IP: `10.0.1.80` (verify current value)
* Wazuh version: `4.14.7` (verify installed version)
* Main test endpoint: `agent-linux-1`
* Endpoint private IP: `10.0.1.237` (verify current value)
* Endpoint operating system: Ubuntu (record the exact version)

## 3. Log Ingestion Test

### Procedure

1. Checked that the Wazuh agent service was running.
2. Reviewed recent authentication logs on the Ubuntu endpoint.
3. Generated a normal administrative event using `sudo whoami`.
4. Searched the Wazuh dashboard for a corresponding event.

### Results

* Local log entry found: Yes
* Corresponding event visible in Wazuh: Yes
* Event timestamp: Oct 11, 2026 @ 02:58:46.883
* Agent name or ID: agent-linux-1
* Rule ID and description: 5402 - Successful sudo to ROOT executed

### Explanation

Log ingestion allows endpoint activity to be collected and reviewed centrally. The Wazuh agent forwards configured logs to the manager, where events are analysed using decoders and rules.

## 4. File Integrity Monitoring Test

### Configuration

* Monitored endpoint: `agent-linux-1`
* Monitored directory: `/home/ubuntu/socwatch-fim-test`
* Test file: `test-file.txt`
* Monitoring mode: Real-time
* Configuration file: `/var/ossec/etc/ossec.conf`

### Procedure

1. Created the test directory and an initial test file.
2. Added the directory to the existing FIM configuration.
3. Restarted the Wazuh agent and verified its service status.
4. Modified the test file.
5. Searched the Wazuh dashboard for a file-change event.

### Results

* Agent service running after configuration: /home/ubuntu/socwatch-fim-test (Real-time mode enabled)
* File modification performed: Yes
* FIM event visible in Wazuh: Yes
* Event timestamp: Oct 11, 2026 @ 05:21:49.108
* Event description: Integrity checksum changed.
* Rule ID: 550

### Technical Explanation

FIM records a baseline of monitored file attributes, including cryptographic checksums. When a monitored file changes, Wazuh compares its attributes with the stored baseline and can generate an event or alert describing the change.

## 5. Evidence

* `W5D1_1_Three_Agents_Active.png`
* `W5D1_2_Linux_Log_Ingestion.png`
* `W5D1_3_Linux_Log_Ingestion_Dashboard.png`
* `W5D1_4_Windows_Log_Ingestion.png`
* `W5D1_5_FIM_Test_File.png`
* `W5D1_6_FIM_Config.png`
* `W5D1_7_FIM_Alert.png`

## 6. Issues and Troubleshooting



## 7. Conclusion


