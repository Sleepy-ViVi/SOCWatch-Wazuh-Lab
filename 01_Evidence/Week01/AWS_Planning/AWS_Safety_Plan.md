# AWS Safety Plan

## Current Status

AWS account:
Created

Project infrastructure:
Not deployed during Week 1

## Planned Infrastructure

- 1 Wazuh manager
- 1 Ubuntu agent
- 1 Rocky/RHEL agent
- 1 Windows Server agent

## Cost Controls

- Use the instance sizes specified by the project brief.
- Avoid unnecessary AWS resources.
- Monitor AWS usage and billing.
- Stop instances when they are not required, where appropriate.
- Do not create additional resources unless they are required by the project.

## Network Security

- SSH limited to my public IP /32.
- HTTPS limited to my public IP /32.
- RDP limited to my public IP /32.
- Wazuh ports 1514 and 1515 limited to the VPC CIDR.
- No unnecessary public ports.

## Credential Security

- Do not upload private SSH keys.
- Do not place passwords in screenshots.
- Do not place credentials in GitHub or other public repositories.