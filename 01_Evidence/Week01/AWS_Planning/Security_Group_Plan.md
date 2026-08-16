# AWS Security Group Plan

## Administrative Access

### SSH
Port: 22
Protocol: TCP
Source: My public IP /32
Purpose: Linux administration

### HTTPS
Port: 443
Protocol: TCP
Source: My public IP /32
Purpose: Wazuh Dashboard

### RDP
Port: 3389
Protocol: TCP
Source: My public IP /32
Purpose: Windows Server administration

## Wazuh Agent Communication

### Agent Events
Port: 1514
Protocol: TCP
Source: VPC CIDR
Purpose: Wazuh agent security events

### Agent Enrollment
Port: 1515
Protocol: TCP
Source: VPC CIDR
Purpose: Wazuh agent enrollment

## Security Restrictions

SSH, HTTPS and RDP must not be opened to 0.0.0.0/0

Administrative access must be restricted to my public IP /32

Wazuh agent ports must only be accessible from the VPC CIDR