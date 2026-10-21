# SOCWatch - Wazuh SOC Monitoring Lab

## 1. Introduction

SOCWatch is a security monitoring lab developed using Amazon Web Services (AWS) and Wazuh. The project demonstrates how a centralized security monitoring platform can collect endpoint events, identify potential security issues, and present findings through a dashboard.

The lab uses Linux and Windows endpoints to explore common security monitoring tasks in a controlled environment.

## 2. Project Objectives

The main objectives were to:

- Deploy a Wazuh monitoring environment on AWS EC2.
- Connect Linux and Windows endpoints to the Wazuh Manager.
- Verify endpoint log collection and centralized event visibility.
- Test File Integrity Monitoring (FIM).
- Review vulnerability detection results.
- Generate and analyze authentication failure events.
- Document the architecture, evidence and troubleshooting process.

## 3. Architecture and Environment

The lab was deployed in the AWS Mumbai Region (`ap-south-1`) using a dedicated VPC and subnet.

The environment consists of a Wazuh Manager, Indexer and Dashboard together with three endpoint systems:

- Ubuntu Linux endpoint
- RHEL Linux endpoint
- Windows Server 2022 endpoint

The Wazuh agents communicate with the Manager using its private IP address. The Indexer stores security data and the Dashboard provides an interface for reviewing alerts and monitoring results.

Refer to `06_Architecture/` for the network configuration and architecture diagram.

## 4. Implementation

Implementation included provisioning the AWS infrastructure, deploying the Wazuh components, enrolling endpoint agents and verifying communication between the endpoints and Manager.

Configuration and deployment challenges were addressed during the process. The troubleshooting records document the principal issues, their causes and the corrective actions taken.

## 5. Security Testing

The lab included the following monitoring tests:

- **Log ingestion:** Checked whether endpoint events appeared in the Wazuh Dashboard.
- **File Integrity Monitoring:** Modified a test file and checked for a corresponding integrity alert.
- **Vulnerability detection:** Reviewed vulnerability findings associated with endpoint software inventory.
- **Authentication monitoring:** Generated controlled SSH authentication failures and examined the resulting security events.

The detailed procedures, timestamps, alert information and screenshot references are recorded in the relevant weekly notes and `02_Screenshots`.

## 6. Challenges and Solutions

The main challenges included EC2 storage requirements, insufficient memory for the initial Manager configuration, SSH session disconnections, agent configuration errors, and Linux service management warnings.

These issues were addressed through configuration changes and troubleshooting. The full issue descriptions and resolutions are maintained in `04_Troubleshooting/`.

## 7. Limitations and Future Improvements

The lab was developed with limited cloud resources, which affected the initial Manager configuration. Bypassing the Wazuh installer's hardware check also means that resource usage and service stability should be monitored.

Possible future improvements include increasing available resources, expanding detection use cases, strengthening alert analysis and adding further testing and reporting.

## 8. Conclusion

The SOCWatch project provided practical experience with cloud infrastructure, endpoint monitoring, centralized event collection and basic security detection using Wazuh. It also demonstrated the importance of validating configurations, investigating errors, maintaining evidence and documenting technical decisions.

## 9. References

**Amazon Web Services (AWS) Documentation:**
* [Amazon EC2 User Guide for Linux Instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
* [Amazon VPC User Guide and Subnet Basics](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
* [AWS Security Groups for Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-security-groups.html)

**Wazuh Installation and Core Deployment:**
* [Wazuh Central Components Installation Guide](https://documentation.wazuh.com/current/installation-guide/index.html)
* [Wazuh Agent Deployment Guide (Linux and Windows)](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html)
* [Wazuh Agent Enrollment Methods](https://documentation.wazuh.com/current/user-manual/agent/agent-enrollment/enrollment-methods/index.html)

**Wazuh Capabilities and Security Modules:**
* [Wazuh File Integrity Monitoring (FIM)](https://documentation.wazuh.com/current/user-manual/capabilities/file-integrity/index.html)
* [Wazuh Vulnerability Detection Module](https://documentation.wazuh.com/current/user-manual/capabilities/vulnerability-detection/index.html)
* [Wazuh Syscollector Module](https://documentation.wazuh.com/current/user-manual/capabilities/system-inventory/index.html)
* [Wazuh ossec.conf Reference Guide](https://documentation.wazuh.com/current/user-manual/reference/ossec-conf/index.html)