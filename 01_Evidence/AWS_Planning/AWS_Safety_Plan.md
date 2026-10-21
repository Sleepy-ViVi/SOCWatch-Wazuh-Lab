# AWS Safety Plan

## 1. Project Status

**Project:** SOCWatch - Wazuh SOC Monitoring Lab  
**Cloud Provider:** Amazon Web Services (AWS)  
**AWS Region:** Asia Pacific (Mumbai) - `ap-south-1`  
**Project Phase:** Week 7 - Final Review, Testing and Documentation

The AWS environment has been provisioned for the Wazuh SOC monitoring project. The infrastructure consists of one central Wazuh manager and three endpoint instances running different operating systems.

The current focus is to verify the infrastructure, review security configurations, resolve outstanding issues, monitor AWS costs and finalise project documentation.

Infrastructure deployment does not automatically confirm that every Wazuh service or endpoint connection is functioning correctly. Service health and agent connectivity must be verified separately.

## 2. AWS Infrastructure

### Network Configuration

| Resource | Configuration |
|---|---|
| VPC Name | `SOCWatch-Wazuh-VPC` |
| VPC CIDR | `10.0.0.0/16` |
| Subnet Name | `SOCWatch-Wazuh-Subnet` |
| Subnet CIDR | `10.0.1.0/24` |
| Availability Zone | `ap-south-1a` |
| Security Group | `SOCWatch-Wazuh-SG` |
| AWS Region | `ap-south-1` |

All four EC2 instances are intended to communicate within the same VPC and subnet.

The Wazuh agents must use the manager's private IP address for agent communication and enrolment.

### Planned and Deployed Instances

| Instance | Purpose | Operating System | Intended Instance Type |
|---|---|---|---|
| `wazuh-manager-2` | Wazuh manager, indexer and dashboard | Ubuntu Server 24.04 LTS | `c7i-flex.large` |
| `agent-linux-1` | Linux endpoint monitoring | Ubuntu | `t3.micro` |
| `agent-linux-2` | Linux endpoint monitoring | Red Hat Enterprise Linux 9 | `t3.micro` |
| `agent-windows-1` | Windows endpoint monitoring | Windows Server 2022 | `t3.small` |

**Implementation note:** The Wazuh manager was provisioned using `c7i-flex.large` because `t3.medium` was unavailable for the selected account configuration. The deployed configuration differs from the original project specification and should be documented as a resource constraint.

The exact deployed instance types, operating systems, private IP addresses, storage allocations and instance states are recorded separately in the AWS instance inventory.

## 3. Cost Controls

AWS resources must be managed carefully to reduce unnecessary charges throughout the project.

The following controls are applied:

- An AWS Budget of $5 per month is configured.
- Budget notifications are configured at 20%, 60%, and 100% of the budget.
- Actual cost monitoring is enabled through the configured budget notifications.
- AWS billing and usage information is reviewed regularly.
- Instances are stopped when they are not required for testing or demonstrations.
- Unnecessary AWS resources are not created.
- Storage volumes, public IPv4 addresses, snapshots and other potentially chargeable resources are reviewed.
- Instance types are selected according to the project requirements and available account options.

Stopping an EC2 instance does not necessarily eliminate all AWS charges. Attached storage and other retained resources may continue to incur costs.

Before starting an instance for testing, its current state, storage configuration and expected resource usage should be reviewed.

## 4. Network Security

The AWS security group follows the principle of least privilege by restricting administrative access and limiting Wazuh communication to the required network.

### Inbound Security Group Rules

| Port | Protocol | Source | Purpose |
|---|---|---|---|
| 22 | TCP | Current public IP `/32` | SSH administration |
| 443 | TCP | Current public IP `/32` | HTTPS dashboard access |
| 3389 | TCP | Current public IP `/32` | Windows Remote Desktop |
| 1514 | TCP | VPC CIDR `10.0.0.0/16` | Wazuh agent communication |
| 1515 | TCP | VPC CIDR `10.0.0.0/16` | Wazuh agent enrolment |

### Network Safety Rules

- SSH, HTTPS and RDP access must be restricted to the authorised public IP address using `/32` CIDR notation.
- Administrative ports must not be exposed to `0.0.0.0/0`.
- Wazuh ports 1514 and 1515 must remain restricted to the VPC CIDR.
- The Wazuh agents must communicate with the manager through its private IP address.
- Unnecessary inbound rules must be removed.
- Security group rules must be reviewed if the public IP address changes.
- Public IP addresses and remote access configurations must be checked before administrative connections are attempted.

### Internet Connectivity

An Internet Gateway and a route for external connectivity are configured for the VPC.

The route table includes a default route to the Internet Gateway to support the required external connectivity.

The Internet Gateway does not, by itself, make every instance publicly accessible. Access also depends on the instance's addressing, routing, security group rules and other applicable network controls.

The security group must continue to restrict administrative access to the authorised public IP address.

## 5. Credential Security

Credentials and private keys must be protected throughout the project.

The following rules apply:

- Private SSH keys must never be uploaded to GitHub.
- AWS access keys, passwords, tokens and other secrets must not be committed to the repository.
- Passwords must not appear in screenshots or publicly shared documentation.
- Wazuh administrator credentials must be stored securely.
- Sensitive information must be removed or obscured before screenshots are shared.
- SSH private keys must be stored locally in a protected location.
- Credentials must not be included in troubleshooting logs or public report files.
- Sensitive configuration files must remain outside the public repository.

The project repository's `.gitignore` file is configured to exclude sensitive files and common credential related file patterns. This does not replace the need to check staged files and repository history before publishing changes.

## 6. Storage and Instance Safety

The EC2 instances must be checked for storage and configuration issues before testing or demonstrations.

The following checks should be performed:

- Confirm that each instance has the expected root volume.
- Check available disk space on the Wazuh manager.
- Review EC2 instance status checks.
- Confirm the expected instance type and operating system.
- Check that the manager has sufficient resources for its installed services.
- Verify that important configuration files and project evidence are preserved.
- Review attached volumes and their deletion settings before making changes.

The Wazuh manager's storage and service health must be verified after starting the instance. If storage or service errors occur, the issue should be investigated and documented before further changes are made.

Important evidence and configuration files should not be deleted as part of routine troubleshooting.

## 7. Monitoring and Troubleshooting

During the final review, the following items must be checked:

- AWS instance states and status checks.
- EC2 storage configuration and available disk space.
- Wazuh manager, indexer and dashboard service status.
- Agent connectivity and enrolment status.
- Security group inbound rules.
- AWS billing and budget notifications.
- Any outstanding issues affecting the final demonstration.

Troubleshooting activities must be recorded in the project troubleshooting log.

Each entry should include the issue, symptoms, investigation, corrective action, verification result and relevant screenshot reference.

An issue must not be marked as resolved until the result has been verified.

## 8. Week 7 Final Safety Checklist

| Check | Status |
|---|---|
| AWS budget and notifications reviewed | Completed |
| EC2 instance inventory updated | Completed |
| Security group rules verified | Completed |
| Administrative ports restricted to the authorised IP | Completed |
| Wazuh ports restricted to the VPC CIDR | Completed |
| Private keys and credentials excluded from GitHub | Completed |
| Manager storage and service health verified | Completed |
| All three agents checked for connectivity | Completed |
| Outstanding issues documented | Completed |
| Unnecessary AWS resources reviewed | Completed |

## 9. Documentation and Evidence

The AWS safety configuration and supporting evidence are maintained in the `SOCWatch-Wazuh-Lab` project repository.

Relevant project locations include:

- `01_Evidence/` - Supporting project evidence.
- `02_Screenshots/` - Weekly review screenshots.
- `03_Report/` - Final project report.
- `04_Troubleshooting/` - Troubleshooting records.
- `05_Weekly_Notes/` - Weekly progress documentation.
- `06_Architecture/` - AWS and Wazuh architecture.
- `07_Instance_Inventory/` - EC2 instance inventory.
- `README.md` - Main project documentation.

Screenshots should be labelled clearly and must not expose passwords, private keys, access tokens or other sensitive information.

## 10. Final Safety Statement

The AWS environment is managed according to the project's network security, credential protection and cost control requirements.

Before the final demonstration, the AWS configuration, storage health, Wazuh services, agent connectivity and outstanding troubleshooting items must be reviewed.

Any configuration that differs from the original project requirements must be documented accurately.

AWS resources that are no longer required should be stopped or removed when appropriate, after confirming that the necessary evidence and project deliverables have been preserved.