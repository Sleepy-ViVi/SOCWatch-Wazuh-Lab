# Day 01 - Project Planning

**Date:** 11 August 2026
**Student:** Pathirage Vidusha Nuwantha Nuwantha
**Project:** SOCWatch - Wazuh SOC Monitoring Lab
**Project Duration:** 8 weeks

## 1. Project Objective

The objective of this project is to build a small Security Operations Centre (SOC) monitoring lab using Wazuh on AWS.

The lab will collect endpoint logs, display security alerts, test File Integrity Monitoring (FIM), review vulnerability findings and support basic security analysis.

## 2. Final Lab Components

The planned lab consists of:

- One Wazuh Manager
- One Wazuh Indexer
- One Wazuh Dashboard
- One Ubuntu Linux agent
- One Rocky Linux/RHEL agent
- One Windows Server agent
- AWS EC2 infrastructure
- AWS VPC and subnet
- AWS security group

## 3. Required Detection Use Cases

The project must demonstrate the following security monitoring capabilities:

- Log ingestion
- File Integrity Monitoring (FIM)
- Vulnerability detection
- Authentication failure detection

## 4. Core Workflow

The planned project workflow is:

1. Provision the AWS lab.
2. Install Wazuh.
3. Enrol the endpoint agents.
4. Trigger security events.
5. Analyse the resulting alerts.
6. Capture evidence and document findings.

## 5. Week 1 Objective

The objective of Week 1 was to plan the project scope, architecture, evidence structure, instance inventory, risks and AWS setup before deploying the infrastructure.

The planning phase established the foundation for the subsequent implementation and testing stages.

## 6. AWS Account Status — Day 1

**AWS Account:** Created

**AWS Infrastructure:** Not yet deployed

**Planned Infrastructure Deployment:** Week 2

On Day 1 the AWS account had been successfully created. The project infrastructure had not yet been deployed.

The planned infrastructure included the EC2 instances, VPC, subnet and security group required for the Wazuh SOC monitoring lab.

This section records the original project status on Day 1 and is retained as a historical record.

## 7. Questions From the Project Brief

Questions identified during the initial planning phase:

- No questions recorded in this section at the time of writing.

Any questions raised during later implementation should be recorded in the relevant weekly notes or troubleshooting documentation.

## 8. Initial Risks Identified

The following risks were identified during project planning:

- Unexpected AWS usage and costs.
- Incorrect security group configuration.
- Accidental exposure of administrative ports.
- Exposure of passwords, private keys or other credentials.
- Connectivity problems between agents and the Wazuh manager.

These risks were documented for review during infrastructure deployment and subsequent testing.

## 9. Day 1 Work Completed

The following checklist records the original Day 1 planning activities.

- [✓] Project brief reviewed
- [✓] Project folder reviewed
- [✓] Evidence structure prepared
- [✓] Report outline prepared
- [✓] Instance inventory prepared
- [✓] Architecture draft prepared
- [✓] Risk list prepared
- [✓] Weekly update format prepared

## 10. Notes and Decisions

Record important decisions made during the initial planning phase.

- The project would use AWS EC2 to host the Wazuh manager and endpoint agents.
- The lab would monitor three endpoints running different operating systems.
- Security alerts and supporting screenshots would be used to demonstrate the required detection capabilities.
- Project documentation and evidence would be maintained throughout the eight week internship.

These notes describe the original project plan. Subsequent implementation decisions and configuration changes are recorded in the relevant project documents.

## 11. Historical Record and Current Project Progress

This document records the initial planning stage of the SOCWatch - Wazuh SOC Monitoring Lab.

The AWS infrastructure, security configuration, monitoring setup and supporting documentation were planned during the initial stage and developed during the subsequent project weeks.

The current implementation status and final verification results are documented separately in the AWS safety plan, instance inventory, troubleshooting records, weekly notes and final report.