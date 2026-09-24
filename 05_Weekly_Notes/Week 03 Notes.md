# Week 03 – Wazuh Manager Deployment

## Objective

Deploy the Wazuh all-in-one manager on AWS EC2 and verify that the manager, indexer, dashboard and Filebeat services are operational.

## Manager Configuration

* Operating System: Ubuntu 24.04.4 LTS
* AWS Region: ap-south-1
* Manager Private IP: 10.0.1.80
* Instance Type: c7i-flex.large
* CPU: 2 vCPU
* RAM: 3.7 GiB
* Root Disk: 29 GB
* Wazuh Version: 4.14.7
* Installation Method: Wazuh all-in-one installation assistant

## Installation

The Wazuh installation assistant was executed using the all-in-one installation method. The hardware check was bypassed using the `-i` option because the available instance configuration had slightly less than the installer's recommended 4 GB RAM requirement.

The installation completed successfully and initialized the Wazuh dashboard.

## Service Verification

The following Wazuh components were verified as active:

* Wazuh Manager
* Wazuh Indexer
* Wazuh Dashboard
* Filebeat

## Dashboard Verification

The Wazuh dashboard was accessed through HTTPS on port 443 using the `admin` account. The generated administrator password was stored securely and was not included in the repository, screenshots or report.

## Evidence Captured

* Wazuh dashboard login
* Wazuh dashboard overview
* Wazuh service status
* Wazuh version
* AWS security group rules

## Security Notes

SSH, HTTPS and RDP administrative access are restricted to the current public IP using `/32` rules. Wazuh agent ports 1514 and 1515 are restricted to the VPC CIDR.

## Project Deviation

The manager instance configuration differs from the original project specification. The deployed manager uses a c7i-flex.large instance with approximately 3.7 GiB RAM and a 29 GB root disk. This configuration was used to continue the lab deployment.

## Week 03 Result

The Wazuh manager, indexer and dashboard were successfully deployed. The central Wazuh services are running and the dashboard is accessible through HTTPS. The environment is ready for agent enrollment in Week 04.
