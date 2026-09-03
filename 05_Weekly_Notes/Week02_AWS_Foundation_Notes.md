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


