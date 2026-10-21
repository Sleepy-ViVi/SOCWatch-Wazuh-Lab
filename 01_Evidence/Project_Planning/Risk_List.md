# Risk Review

**Project:** SOCWatch - Wazuh SOC Monitoring Lab  
**Review Period:** Week 7  
**Purpose:** Review project risks, confirm mitigation measures and document the current risk status before the final demonstration.

## Risk 01 - AWS Cost

**Description:**

AWS resources may generate unexpected charges if they are left running or larger resources are selected than required.

**Mitigation:**

- Use only the AWS resources required for the project.
- Monitor AWS usage and billing.
- Review the configured AWS budget and notifications.
- Stop instances when they are not needed.
- Review storage volumes, public IPv4 addresses and other potentially chargeable resources.

**Status:** Mitigation Implemented - Ongoing Monitoring Required

## Risk 02 - Administrative Port Exposure

**Description:**

SSH, HTTPS or RDP could accidentally be exposed to the entire internet, increasing the risk of unauthorised access.

**Mitigation:**

- Restrict port 22 (SSH) to the authorised public IP `/32`.
- Restrict port 443 (HTTPS) to the authorised public IP `/32`.
- Restrict port 3389 (RDP) to the authorised public IP `/32`.
- Review security group rules regularly.
- Update the authorised IP restriction when the public IP changes.

**Status:** Mitigation Implemented - Continue Monitoring

## Risk 03 - Wazuh Agent Connectivity

**Description:**

Linux or Windows agents may fail to communicate with the Wazuh manager, preventing endpoint events from reaching the central monitoring system.

**Mitigation:**

- Keep the project machines in the intended VPC and subnet.
- Configure agents to communicate with the manager's private IP address.
- Allow TCP ports 1514 and 1515 from the VPC CIDR.
- Verify agent connectivity and status in the Wazuh dashboard.
- Record and resolve connectivity problems in the troubleshooting log.

**Status:** Verified - Continue Monitoring

## Risk 04 - Credential Exposure

**Description:**

Passwords, private SSH keys, tokens or other sensitive information could accidentally be included in screenshots, project files or the public GitHub repository.

**Mitigation:**

- Never upload private SSH keys or passwords to GitHub.
- Do not include credentials in screenshots or submitted evidence.
- Store credentials securely.
- Review files before committing or publishing changes.
- Check that sensitive files are excluded from version control.

**Status:** Mitigation Implemented - Continue Monitoring

## Risk 05 - Incorrect Security Group Rules

**Description:**

Incorrect inbound rules could prevent required communication between the Wazuh manager and its agents or expose unnecessary services.

**Mitigation:**

- Allow only the inbound ports required for the project.
- Restrict administrative access to the authorised public IP `/32`.
- Restrict Wazuh ports 1514 and 1515 to the VPC CIDR.
- Review the security group configuration in the AWS console.
- Remove unnecessary inbound rules.

**Status:** Verified - Continue Monitoring

## Week 7 Final Risk Review

| Risk ID | Risk | Current Status | Follow-up |
|---|---|---|---|
| Risk 01 | AWS Cost | Mitigation implemented | Continue monitoring usage and billing |
| Risk 02 | Administrative Port Exposure | Mitigation implemented | Review restrictions if the public IP changes |
| Risk 03 | Wazuh Agent Connectivity | Verified | Recheck agent health before the final demonstration |
| Risk 04 | Credential Exposure | Mitigation implemented | Review repository changes before publishing |
| Risk 05 | Incorrect Security Group Rules | Verified | Recheck rules before the final demonstration |

## Final Review Notes

The identified risks have been reviewed during Week 7. Mitigation measures have been implemented for AWS cost control, administrative access, credential protection and security group configuration.

Wazuh agent connectivity and security group rules have been marked as verified based on the completed project checks.

Cost monitoring, credential protection and network security remain ongoing responsibilities until the project is handed over.

Any new issues discovered during final testing must be documented, investigated and addressed before the final demonstration.