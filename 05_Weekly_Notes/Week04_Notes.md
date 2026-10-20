# Week 04 - Endpoint Agent Deployment and Enrollment

## 1. Objective

Deploy and enroll the Ubuntu Linux, Red Hat Enterprise Linux (RHEL) and Windows Server endpoints with the central Wazuh manager.

The objectives for this stage were to:

- Configure the Wazuh agent on each endpoint.
- Connect all three endpoints to the intended Wazuh manager.
- Verify agent connectivity and status in the Wazuh dashboard.
- Check the local agent service status where applicable.
- Capture screenshots documenting successful enrollment.

---

## 2. Wazuh Manager Configuration

The endpoint agents are configured to communicate with the Wazuh manager.

| Property | Configuration |
|---|---|
| Manager Private IP | `10.0.1.80` |
| Wazuh Version | `4.14.7` |
| Agent Communication Port | TCP `1514` |
| Agent Enrollment Port | TCP `1515` |

**Technical note:** TCP port `1514` is used for Wazuh agent communication, while TCP port `1515` is used for agent enrollment in the standard configuration.

The endpoints and manager should be able to communicate through the configured AWS network and security-group rules.

---

## 3. Endpoint Inventory

The following table records the three endpoints included in this deployment stage.

| Endpoint | Operating System | Private IPv4 Address | Expected Agent Name |
|---|---|---|---|
| Linux 1 | Ubuntu Server | `10.0.1.237` | `agent-linux-1` |
| Linux 2 | Red Hat Enterprise Linux 9.x | `10.0.1.177` | `agent-linux-2` |
| Windows 1 | Windows Server 2022 | `10.0.1.115` | `agent-windows-1` |

---

## 4. Work Completed

The following activities were recorded during the endpoint deployment stage:

- Set up the Wazuh agents on the three endpoints.
- Configured the endpoints to connect to the Wazuh manager.
- Checked the enrolled agents in the Wazuh dashboard.
- Recorded screenshots of the agent details and local service status.

---

## 5. Agent Verification Results

| Agent | Expected Agent Name | Reported Status | Final Verification |
|---|---|---|---|
| Ubuntu Linux | `agent-linux-1` | Active (running) | Confirm against dashboard and local service evidence |
| RHEL Linux | `agent-linux-2` | Active (running) | Confirm against dashboard and local service evidence |
| Windows Server | `agent-windows-1` | Active (running) | Confirm against dashboard and local service evidence |

### Verification Requirements

For each endpoint, confirm that:

1. The agent appears in the Wazuh dashboard.
2. The displayed agent name matches the expected name.
3. The dashboard reports the agent as active or connected.
4. The endpoint's local Wazuh agent service is running, if checked.
5. The agent is communicating with the intended manager.

---

## 6. Evidence Captured

`W4D3_7_Three_Active_Agents_Details.png`
`W4D3_8_Agent_Linux1_Service.png`
`W4D3_9_Agent_Linux2_Service.png`
`W4D3_10_Agent_Windows_Service.png`

### Evidence Checklist

- [✓] Confirm that all four screenshot files exist.
- [✓] Confirm that the screenshots are readable.
- [✓] Confirm that the agent names match the endpoint inventory.
- [✓] Confirm that the dashboard screenshot shows the actual agent statuses.
- [✓] Confirm that the service screenshots show the relevant service states.
- [✓] Store the evidence in the appropriate project screenshot folder.

---

## 7. Technical Explanation

Wazuh agents run on monitored endpoints and send configured security information to the central Wazuh manager.

The manager processes the incoming information and makes relevant alerts and agent information available through the Wazuh platform.

In the standard configuration used by this project:

- **TCP 1514:** Used for agent-to-manager communication.
- **TCP 1515:** Used for agent enrollment.

Successful enrollment and communication allow the manager to receive information from the Ubuntu, RHEL, and Windows endpoints.

Agent connectivity depends on the local agent configuration, network connectivity and the applicable AWS security-group rules.

---

## 8. Troubleshooting and Issues

Record any problems encountered during agent deployment or enrollment.

| Issue | Action Taken | Outcome |
|---|---|---|
| No issue recorded in this section | Not applicable | Update if troubleshooting was required |

---

## 9. Week 04 Result

The Week 4 deployment stage focused on enrolling 3 endpoint agents with the Wazuh manager:

- Ubuntu Linux - `agent-linux-1`
- Red Hat Enterprise Linux - `agent-linux-2`
- Windows Server - `agent-windows-1`

---

## 10. Next Steps

Following successful agent enrollment:

1. Confirm that all three agents remain connected to the intended manager.
2. Verify that endpoint events are reaching the Wazuh platform.
3. Test the required detection use cases, including log ingestion and File Integrity Monitoring.
4. Investigate vulnerability detection and authentication failure alerts.
5. Capture evidence for each tested use case.
6. Record the test procedures, results and any troubleshooting in the appropriate weekly notes.