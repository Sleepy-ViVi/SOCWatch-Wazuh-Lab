# Week 03 - Wazuh Manager Deployment

## 1. Objective

Deploy the Wazuh all in one security monitoring platform on an AWS EC2 instance and verify the main components, including the Wazuh manager, indexer, dashboard and Filebeat.

## 2. Environment Configuration

| Property | Configuration |
|---|---|
| Cloud Provider | Amazon Web Services (AWS) |
| AWS Region | Asia Pacific (Mumbai) - `ap-south-1` |
| Manager Instance | `wazuh-manager-2` |
| Operating System | Ubuntu Server 24.04 LTS |
| Manager Private IP | `10.0.1.80` |
| Instance Type | `c7i-flex.large` |
| CPU | 2 vCPUs |
| Memory | 4 GiB |
| Root Storage | 30 GB |
| Wazuh Version | `4.14.7` |
| Installation Method | Wazuh all-in-one installation assistant |

## 3. Installation

The Wazuh installation assistant was executed using the all-in-one installation method.

The installer's hardware check was bypassed using the `-i` option because the available instance configuration had slightly less memory than the installer's recommended 4 GB requirement.

The installation was recorded as completing successfully and initializing the Wazuh dashboard.

The main components installed were:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Filebeat

**Installation evidence limitation:** The original installation-time screenshots and logs were not retained. The available evidence documents the system after installation.

## 4. Service Verification

The following components were reported as active during verification:

- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard
- Filebeat

The service states were checked using Linux terminal commands.

Retain the active status for each component only where the captured terminal output supports it.

## 5. Dashboard Verification

The Wazuh dashboard was accessed through a web browser using HTTPS on port `443`.

The `admin` account was used to access the dashboard.

The generated administrator password was stored securely and was not included in the GitHub repository, screenshots or report.

Dashboard verification included:

- Dashboard login
- Dashboard overview
- Access through HTTPS

## 6. Evidence Captured

- `W4D3_3_Wazuh_Dashboard_Login.png`
- `W4D3_4_Wazuh_Dashboard_Overview_2.png`
- `W4D3_5.1_Manager_Services_Active.png`
- `W4D3_5.2_Manager_Services_Active.png`

## 7. Security Configuration

The documented security-group configuration specifies the following access restrictions:

- SSH access is restricted to the authorised public IP address using a `/32` rule.
- HTTPS access is restricted to the authorised public IP address using a `/32` rule.
- RDP access is restricted to the authorised public IP address using a `/32` rule.
- Wazuh agent communication ports TCP `1514` and `1515` are restricted to the VPC CIDR.

The expected VPC CIDR is `10.0.0.0/16`.

## 8. Project Deviation

The deployed manager configuration differs from the originally specified `t3.medium` instance.

The deployed instance uses:

- Instance type: `c7i-flex.large`
- CPU: 2 vCPUs
- Memory: Approximately 3.7 GiB, as recorded
- Root storage: Approximately 29 GB, as recorded

The installation assistant's hardware check was bypassed because the available memory was slightly below the installer's recommended requirement.

## 9. Week 03 Result

The Wazuh all-in-one installation was recorded as completing successfully. The manager, indexer, dashboard and Filebeat were reported as active and the dashboard was accessed through HTTPS.

The evidence includes dashboard screenshots and terminal screenshots documenting service status.

The manager configuration differs from the original project specification and the deviation has been recorded.

The environment can be considered ready for agent enrollment once the manager's current operational status and the relevant service checks have been confirmed.

## 11. Next Steps

The next implementation stage is to:

1. Enroll the Linux and Windows endpoint agents.
2. Confirm that each agent connects to the intended Wazuh manager.
3. Verify that endpoint events are reaching the manager.
4. Capture dashboard evidence showing agent status.
5. Record any connectivity issues and their resolutions.
6. Update the relevant weekly notes and troubleshooting documentation.