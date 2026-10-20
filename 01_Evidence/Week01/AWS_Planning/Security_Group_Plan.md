# AWS Security Group Plan

## 1. Administrative Access

Administrative ports are restricted to my current public IP address using `/32` CIDR notation.

| Service | Port | Protocol | Source | Purpose |
|---|---:|---|---|---|
| SSH | 22 | TCP | My public IP `/32` | Linux administration |
| HTTPS | 443 | TCP | My public IP `/32` | Wazuh Dashboard access |
| RDP | 3389 | TCP | My public IP `/32` | Windows Server administration |

## 2. Wazuh Agent Communication

Wazuh agent communication is restricted to the project's Virtual Private Cloud (VPC).

**VPC CIDR:** `10.0.0.0/16`

| Service | Port | Protocol | Source | Purpose |
|---|---:|---|---|---|
| Agent Events | 1514 | TCP | `10.0.0.0/16` | Wazuh agent security event communication |
| Agent Enrollment | 1515 | TCP | `10.0.0.0/16` | Wazuh agent enrollment |

Wazuh agents communicate with the manager using its private IP address.

## 3. Security Restrictions

- SSH, HTTPS and RDP must not be exposed to `0.0.0.0/0`.
- Administrative access must be restricted to my current public IP address using `/32` CIDR notation.
- Wazuh ports 1514 and 1515 must only accept inbound connections from the VPC CIDR.
- Unnecessary inbound rules must not be added.
- The security group must be reviewed whenever network access requirements or the public IP address change.
- All inbound rules must be checked against the actual AWS security group configuration.

## 4. Security Verification

The AWS security group configuration has been reviewed against the project's network security requirements.

| Verification Item | Status |
|---|---|
| SSH restricted to the authorised public IP `/32` | Verified |
| HTTPS restricted to the authorised public IP `/32` | Verified |
| RDP restricted to the authorised public IP `/32` | Verified |
| Port 1514 restricted to the VPC CIDR | Verified |
| Port 1515 restricted to the VPC CIDR | Verified |
| Unnecessary inbound rules reviewed | Verified |

## 5. Network Configuration

| Resource | Name | ID / CIDR |
|---|---|---|
| VPC | SOCWatch-Wazuh-VPC | `vpc-01b73959cc4efd434` |
| Subnet | SOCWatch-Wazuh-Subnet | `subnet-0b173f861128729cd` |
| Security Group | SOCWatch-Wazuh-SG | `sg-03ea4f434a66a7677` |
| VPC CIDR | - | `10.0.0.0/16` |
| Subnet CIDR | - | `10.0.1.0/24` |

## 6. Security Objective

The purpose of this configuration is to minimise unnecessary network exposure while allowing authorised administration and communication between the Wazuh manager and its agents.