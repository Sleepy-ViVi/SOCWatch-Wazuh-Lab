AWS Region selected: ap-south-1
Manager instance created successfully.
t3.medium was unavailable under the current AWS Free plan.
t3.small was selected as a temporary alternative.
Manager storage configured as 30 GiB gp3.
Instance was stopped when not actively being used to reduce compute costs.
The EBS volume remains attached and may continue to incur storage charges while the instance is stopped.


# Wazuh Manager EC2 Instance

Instance Name: wazuh-manager
Operating System: Ubuntu Server 24.04 LTS
Instance Type: t3.small
Private IPv4: 10.0.1.159
VPC: SOCWatch-Wazuh-VPC (10.0.0.0/16)
Subnet: SOCWatch-Wazuh-Subnet (10.0.1.0/24)
Availability Zone: ap-south-1a
Security Group: SOCWatch-Wazuh-SG
Key Pair: SOCWatch-Wazuh-Key
Storage: 30 GiB gp3

Cost Control:
The instance was stopped when not actively being used to avoid unnecessary EC2 compute usage. The attached EBS volume remains allocated while the instance is stopped.


# EC2 Endpoint Deployment – agent-linux-1

Instance Name: agent-linux-1
Operating System: Ubuntu Server 24.04 LTS
Instance Type: t3.micro
Private IPv4 Address: 10.0.1.237
VPC: SOCWatch-Wazuh-VPC (10.0.0.0/16)
Subnet: SOCWatch-Wazuh-Subnet (10.0.1.0/24)
Availability Zone: ap-south-1a
Security Group: SOCWatch-Wazuh-SG
Storage: 8 GiB gp3

Configuration Note:
The project specification originally recommended Ubuntu Server 22.04 LTS. The standard Ubuntu 22.04 AMI was not available in the launch options encountered. An available Ubuntu 22.04 AMI included Microsoft SQL Server 2022 Standard and was not used to avoid unnecessary software and potential additional costs. Ubuntu Server 24.04 LTS was selected instead.


# EC2 Endpoint 2 Deployment – Agent-linux-2 

Instance Name: agent-linux-2
Operating System: Red Hat Enterprise Linux 9
Instance Type: t3.micro
Private IPv4 Address: 10.0.1.177
VPC: SOCWatch-Wazuh-VPC (10.0.0.0/16)
Subnet: SOCWatch-Wazuh-Subnet (10.0.1.0/24)
Availability Zone: ap-south-1a
Security Group: SOCWatch-Wazuh-SG
Storage: 10 GiB gp3

The second Linux endpoint was created using Red Hat Enterprise Linux 9.8 and a t3.micro EC2 instance. It was deployed inside SOCWatch-Wazuh-VPC and SOCWatch-Wazuh-Subnet using the existing SOCWatch-Wazuh-SG security group. The instance was assigned the private IP address 10.0.1.177. During the initial deployment attempt, an 8 GiB root volume caused an AMI snapshot size error. The issue was resolved by increasing the root volume to 10 GiB.


# EC2 Endpoint Deployment – Agent-Windows-1

Instance Name: agent-windows-1
Operating System: Windows Server 2022 Base
Instance Type: t3.small
Private IPv4 Address: 10.0.1.115
VPC: SOCWatch-Wazuh-VPC (10.0.0.0/16)
Subnet: SOCWatch-Wazuh-Subnet (10.0.1.0/24)
Availability Zone: ap-south-1a
Security Group: SOCWatch-Wazuh-SG
Storage: 30 GiB gp3

The Windows endpoint AMI selection was reviewed before deployment. Microsoft Windows Server 2022 Base (64-bit x86) was selected because it matches the project's Windows Server 2022 requirement. SQL Server and Office-preinstalled AMIs were excluded because those additional applications were unnecessary for the Wazuh SOC monitoring lab.