# Week 01 Risk List

## Risk 01 — AWS Cost

Description:
AWS resources may generate unexpected charges if they are left running
or larger resources are selected than required.

Mitigation:
Use only the required resources, monitor AWS usage and billing, and stop
instances when they are not needed.

Status:
Open

## Risk 02 — Administrative Port Exposure

Description:
SSH, HTTPS or RDP could accidentally be exposed to the entire internet.

Mitigation:
Restrict ports 22, 443 and 3389 to my public IP /32.

Status:
Open

## Risk 03 — Wazuh Agent Connectivity

Description:
Agents may fail to communicate with the Wazuh manager.

Mitigation:
Keep all machines in the same VPC and subnet and use the manager's
private IP for agent communication.

Status:
Open

## Risk 04 — Credential Exposure

Description:
Passwords, private keys or other credentials could accidentally be
included in screenshots or project files.

Mitigation:
Do not include passwords, private SSH keys, tokens or other secrets
in screenshots, public repositories or submitted evidence.

Status:
Open

## Risk 05 — Incorrect Security Group Rules

Description:
Incorrect inbound rules could prevent required communication or expose
unnecessary services.

Mitigation:
Create only the required inbound rules and verify each rule before
deployment.

Status:
Open