# Week 04 — Endpoint Agent Deployment and Enrollment

## Objective

Connect the Ubuntu Linux, RHEL Linux, and Windows Server endpoints to the Wazuh manager and verify their status in the dashboard.

## Wazuh Manager

* Manager private IP: `10.0.1.80`
* Wazuh version: `4.14.7`
* Agent communication port: TCP `1514`
* Agent enrollment port: TCP `1515`

## Endpoint Inventory

| Endpoint  | Operating System    | Private IP   | Expected Agent Name |
| --------- | ------------------- | ------------ | ------------------- |
| Linux 1   | Ubuntu              | `10.0.1.237` | `agent-linux-1`     |
| Linux 2   | RHEL 9.x            | `10.0.1.177` | `agent-linux-2`     |
| Windows 1 | Windows Server 2022 | `10.0.1.115` | `agent-windows-1`   |

Confirm the current IP addresses and operating-system versions before treating this table as final.

## Work Completed

* Set up the three endpoint agents.
* Connected the endpoints to the Wazuh manager.
* Checked the agent list in the Wazuh dashboard.

## Verification Results

Record the current dashboard status for each agent:

* Linux 1: active (running)
* Linux 2: active (running)
* Windows 1: active (running)

Record the local Wazuh agent service status for each endpoint if checked.

## Evidence

* `W4D3_7_Three_Active_Agents_Details.png`
* `W4D3_8_Agent_Linux1_Service.png`
* `W4D3_9_Agent_Linux2_Service.png`
* `W4D3_10_Agent_Windows_Service.png`

## Technical Explanation

The Wazuh agents collect configured endpoint security information and communicate with the Wazuh manager. TCP port 1514 is used for agent communication, while TCP port 1515 supports agent enrollment.

## Result

Complete this section after confirming that all three agents have the expected status in the dashboard and saving the supporting evidence.
