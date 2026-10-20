# Week 02 - AWS Infrastructure Deployment Notes

## 1. AWS Deployment Overview

**AWS Region:** `ap-south-1`  
**VPC:** `SOCWatch-Wazuh-VPC`  
**VPC CIDR:** `10.0.0.0/16`  
**Subnet:** `SOCWatch-Wazuh-Subnet`  
**Subnet CIDR:** `10.0.1.0/24`  
**Availability Zone:** `ap-south-1a`  
**Security Group:** `SOCWatch-Wazuh-SG`

The AWS infrastructure was deployed for the SOCWatch Wazuh SOC Monitoring Lab. The deployment included a Wazuh manager and three endpoint instances running Linux and Windows operating systems.

The following sections document the original instance deployments and the subsequent manager configuration.

---

## 2. Original Wazuh Manager Deployment

**Instance Name:** `wazuh-manager`  
**Operating System:** Ubuntu Server 24.04 LTS  
**Instance Type:** `t3.small`  
**Private IPv4 Address:** `10.0.1.159`  
**VPC:** `SOCWatch-Wazuh-VPC`  
**Subnet:** `SOCWatch-Wazuh-Subnet`  
**Availability Zone:** `ap-south-1a`  
**Security Group:** `SOCWatch-Wazuh-SG`  
**Key Pair:** `SOCWatch-Wazuh-Key`  
**Storage:** 30 GiB gp3

### Instance Selection

The originally intended `t3.medium` instance type was unavailable under the AWS account configuration encountered during deployment. The `t3.small` instance type was selected as a temporary alternative.

### Storage and Cost Management

The manager's storage was configured as a 30 GiB gp3 EBS volume.

The instance was stopped when it was not actively being used to reduce EC2 compute costs. The attached EBS volume remained allocated and could continue to incur storage charges while the instance was stopped.

### Historical Record

This section records the original manager deployment. Its current operational status is terminated.

---

## 3. Linux Endpoint 1 - Ubuntu

**Instance Name:** `agent-linux-1`  
**Operating System:** Ubuntu Server 24.04 LTS  
**Instance Type:** `t3.micro`  
**Private IPv4 Address:** `10.0.1.237`  
**VPC:** `SOCWatch-Wazuh-VPC`  
**Subnet:** `SOCWatch-Wazuh-Subnet`  
**Availability Zone:** `ap-south-1a`  
**Security Group:** `SOCWatch-Wazuh-SG`  
**Storage:** 8 GiB gp3

### Operating System Selection

The project specification originally recommended Ubuntu Server 22.04 LTS.

During deployment, the standard Ubuntu 22.04 AMI was not available among the launch options encountered. An available Ubuntu 22.04 AMI included Microsoft SQL Server 2022 Standard.

To avoid unnecessary software and potential additional costs, Ubuntu Server 24.04 LTS was selected instead.

---

## 4. Linux Endpoint 2 - Red Hat Enterprise Linux

**Instance Name:** `agent-linux-2`  
**Operating System:** Red Hat Enterprise Linux 9.8  
**Instance Type:** `t3.micro`  
**Private IPv4 Address:** `10.0.1.177`  
**VPC:** `SOCWatch-Wazuh-VPC`  
**Subnet:** `SOCWatch-Wazuh-Subnet`  
**Availability Zone:** `ap-south-1a`  
**Security Group:** `SOCWatch-Wazuh-SG`  
**Storage:** 10 GiB gp3

### Deployment Details

The second Linux endpoint was created using Red Hat Enterprise Linux 9.8 on a `t3.micro` EC2 instance.

The instance was deployed inside the project's VPC and subnet using the existing security group.

### Deployment Issue and Resolution

During the initial deployment attempt, an 8 GiB root volume caused an AMI snapshot size error.

The issue was resolved by increasing the root volume to 10 GiB.

This change allowed the instance deployment to proceed with the larger root volume.

---

## 5. Windows Endpoint - Windows Server 2022

**Instance Name:** `agent-windows-1`  
**Operating System:** Windows Server 2022 Base  
**Instance Type:** `t3.small`  
**Private IPv4 Address:** `10.0.1.115`  
**VPC:** `SOCWatch-Wazuh-VPC`  
**Subnet:** `SOCWatch-Wazuh-Subnet`  
**Availability Zone:** `ap-south-1a`  
**Security Group:** `SOCWatch-Wazuh-SG`  
**Storage:** 30 GiB gp3

### AMI Selection

Microsoft Windows Server 2022 Base (64-bit x86) was selected because it matched the project's Windows Server 2022 requirement.

AMIs with SQL Server or Microsoft Office preinstalled were excluded because those additional applications were unnecessary for the Wazuh SOC monitoring lab.

---

## 6. Subsequent Wazuh Manager Configuration

**Instance Name:** `wazuh-manager-2`  
**Operating System:** Ubuntu 24.04.4 LTS  
**Instance Type:** `c7i-flex.large`  
**Private IPv4 Address:** `10.0.1.80`   
**VPC:** `SOCWatch-Wazuh-VPC`  
**Subnet:** `SOCWatch-Wazuh-Subnet`  
**AWS Region:** `ap-south-1`
**Security Group:** `SOCWatch-Wazuh-SG`  
**Storage:** 30 GiB gp3

### Configuration Note

The newer manager configuration uses `c7i-flex.large` rather than the originally intended `t3.medium` or the `t3.small` used in first `wazuh-manager`.

This represents a difference from the original instance specification. The reason for the change is the memory given by the `t3.small` was not enough for the wazuh manager.

**Current operational status:** `wazuh-manager-2` is the active manager used by the endpoint agents.

**Original manager status:** `wazuh-manager` is terminated.

---

## 7. Deployment Issues and Resolutions

| Issue | Resolution or follow-up |
|---|---|
| `t3.medium` unavailable during the original manager deployment | Selected `t3.small` as a temporary alternative. |
| Ubuntu 22.04 AMI selection limitation | Selected Ubuntu Server 24.04 LTS. |
| Red Hat endpoint deployment failed with an 8 GiB root volume | Increased the root volume to 10 GiB. |
| A newer manager configuration uses a different instance type | Documented the newer configuration; confirm the reason for the change and the original manager's status. |
| `t3.small` was not giving enough memory for `wazuh-manager` | Used `c7i-flex.large` and create `wazuh-manager-2`

---

## 8. Cost Management Notes

The following cost management practices were recorded during deployment:

- Stop instances when they are not required, where appropriate.
- Review EC2 instance types and storage allocations.
- Check attached EBS volumes before removing or retaining unused instances.
- Review the AWS billing dashboard periodically.

Stopping an EC2 instance generally stops its instance compute charges, but attached EBS storage and certain other resources continue to incur charges.

---

## 9. Verification Checklist

- [✓] Confirm the active Wazuh manager instance.
- [✓] Confirm the original manager's current status.
- [✓] Confirm the private IP address of the active manager.
- [✓] Confirm the three endpoint instances and their current IP addresses.
- [✓] Verify that the agents are connected to the intended manager.
- [✓] Verify that the Wazuh dashboard is accessible.
- [✓] Verify the current Wazuh version.
- [✓] Review the security group inbound and outbound rules.
- [✓] Review instance and EBS storage costs.
- [✓] Capture screenshots of the current EC2 instances and their statuses.

---

## 10. Week 2 Summary

Week 2 focused on deploying the AWS infrastructure required for the SOCWatch Wazuh SOC Monitoring Lab.

The deployment records cover the original manager, two Linux endpoints, one Windows endpoint and a subsequent manager configuration.

The documented deployment challenges included instance-type availability, operating system image selection and a root-volume size issue. The notes also record the storage and cost management considerations associated with running EC2 instances.