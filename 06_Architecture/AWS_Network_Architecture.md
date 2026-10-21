# AWS Network Architecture - SOCWatch

## 1. Overview

This document describes the AWS network infrastructure used by the SOCWatch Wazuh Security Information and Event Management (SIEM) lab. The environment hosts a central Wazuh server and three endpoint agents within a dedicated Virtual Private Cloud (VPC).

## 2. AWS Network Configuration

| Component | Configuration |
|---|---|
| AWS Region | `ap-south-1` — Mumbai |
| VPC Name | `SOCWatch-Wazuh-VPC` |
| VPC ID | `vpc-01b73959cc4efd434` |
| VPC CIDR | `10.0.0.0/16` |
| Subnet Name | `SOCWatch-Wazuh-Subnet` |
| Subnet ID | `subnet-0b173f861128729cd` |
| Subnet CIDR | `10.0.1.0/24` |
| Availability Zone | `ap-south-1a` |
| Security Group Name | `SOCWatch-Wazuh-SG` |
| Security Group ID | `sg-03ea4f434a66a7677` |

## 3. EC2 Instance Inventory

| Instance | Private IP | Operating System | Role |
|---|---|---|---|
| `wazuh-manager-2` | `10.0.1.80` | Ubuntu 24.04 LTS | Wazuh Manager, Indexer and Dashboard |
| `agent-linux-1` | `10.0.1.237` | Ubuntu 24.04 LTS | Linux endpoint monitoring |
| `agent-linux-2` | `10.0.1.177` | RHEL 9 | Linux endpoint monitoring |
| `Windows-EC2` | `10.0.1.115` | Windows Server 2022 | Windows endpoint monitoring |

## 4. Network Communication and Ports

| Port | Protocol | Purpose | Verification |
|---|---|---|---|
| `1514` | TCP | Wazuh agent communication and event delivery | Manager listener previously reported active |
| `1515` | TCP | Wazuh agent enrollment | Required when using the enrollment service |
| `443` | HTTPS/TCP | Wazuh Dashboard web access | Dashboard access previously reported working |
| `22` | SSH/TCP | Linux instance administration | Intended to be restricted to authorized IPs |
| `3389` | RDP/TCP | Windows instance administration | Intended to be restricted to authorized IPs |

The Wazuh agents are configured to use the Manager's private IP address, `10.0.1.80`, for internal communication. Using private addressing avoids relying on the Manager's public IP for communication between instances in the same VPC.

The Wazuh Dashboard is accessed over HTTPS. Administrative access and agent connectivity depend on the applicable security group rules and service configurations.

## 5. Security Group Design

The security group `SOCWatch-Wazuh-SG` is intended to control network traffic to and from the EC2 instances.

The intended inbound restrictions are:

- **TCP 1514:** Allow Wazuh agent communication from the required internal network.
- **TCP 1515:** Allow enrollment traffic from the required internal network when enrollment is needed.
- **TCP 443:** Permit Dashboard access only from authorized sources.
- **TCP 22:** Restrict SSH access to the authorized administrator's IP address.
- **TCP 3389:** Restrict RDP access to the authorized administrator's IP address.

## 6. Network Design Notes

- **Private communication:** Agents use the Manager's private IP address, `10.0.1.80`, for communication within the VPC.
- **Address persistence:** An EC2 instance's private IPv4 address normally remains associated with its network interface across stop/start operations.
- **Least privilege access:** Administrative and Wazuh ports should only be reachable from the sources that require them.
- **Service availability:** Correct security group rules alone do not guarantee connectivity. Routing, service status and host configuration must also be correct.

## 7. References

- [AWS Security Group Rules](https://docs.aws.amazon.com/vpc/latest/userguide/security-group-rules.html)
- [Wazuh Agent Enrollment Requirements](https://documentation.wazuh.com/current/user-manual/agent/agent-enrollment/requirements.html)
- [Wazuh Architecture](https://documentation.wazuh.com/current/getting-started/architecture.html)