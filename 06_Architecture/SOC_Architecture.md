# SOC Architecture - SOCWatch Wazuh Lab

## 1. Overview

This document describes the logical architecture of the SOCWatch Security Operations Center (SOC) monitoring lab. The environment uses Wazuh to collect endpoint security data, analyze events, detect suspicious activity and display alerts through a web based dashboard.

The lab uses an **all-in-one Wazuh deployment** on an AWS EC2 instance with three endpoint agents monitoring Linux and Windows systems.

## 2. Core Wazuh Components

The Wazuh Manager, Indexer and Dashboard are hosted on the Manager EC2 instance at private IP `10.0.1.80`.

| Component | Role | Environment Status |
|---|---|---|
| **Wazuh Manager** | Receives endpoint events, analyzes logs, applies detection rules and generates alerts. | The `wazuh-remoted` service is active and listening on TCP port `1514`. |
| **Wazuh Indexer** | Indexes and stores security data so it can be searched and analyzed. | Managed through the `wazuh-indexer` systemd service on the Manager instance. |
| **Wazuh Dashboard** | Provides the web interface for reviewing alerts, agent status and security events. | Managed through the `wazuh-dashboard` systemd service and accessible over HTTPS on port `443`. |

The three central components share one EC2 host in this lab. This simplifies deployment, but it also means that a failure of the Manager instance can affect the entire central monitoring platform.

## 3. Endpoint Agents

Wazuh agents run on monitored endpoints and send security data to the Manager for analysis.

| Agent Name | Operating System | Private IP | Agent Version |
|---|---|---|---|
| `agent-linux-1` (Agent ID: `002`) | Ubuntu 24.04.4 LTS | `10.0.1.237` | `4.14.8` |
| `agent-linux-2` (Agent ID: `003`) | Red Hat Enterprise Linux 9.8 | `10.0.1.177` | `4.14.8` |
| `Windows-EC2` (Agent ID: `004`) | Microsoft Windows Server 2022 Datacenter | `10.0.1.115` | `4.8.0` |

**Agent responsibilities:**
- Collect configured system and security logs.
- Monitor selected files and directories for integrity changes.
- Collect system inventory and other configured endpoint information.
- Send security events to the Wazuh Manager for analysis.

The exact data collected depends on the agent configuration and the monitoring features enabled on each endpoint.

## 4. Communication and Network Ports

The agents communicate with the Manager using its private IP address, `10.0.1.80`.

| Port | Protocol | Purpose | Status |
|---|---|---|---|
| `1514` | TCP | Agent communication and event transmission. | The Manager listener is active. |
| `1515` | TCP | Agent enrollment and registration. | Enrollment was completed during initial setup. |
| `443` | HTTPS/TCP | Web access to the Wazuh Dashboard. | Dashboard access is working. |

Port `1514` carries ongoing agent communications. Port `1515` is used for enrollment when the configured enrollment method requires it. These are separate functions in Wazuh's default configuration.

**Network security:** Agent traffic should use the Manager's private IP for communication within the AWS network. Security group rules should allow only the required traffic from authorized sources. Dashboard access should be restricted to approved users and network sources.

## 5. Logical Data Flow

```text
+----------------------+       +----------------------+
| Ubuntu Agent         |       | RHEL Agent           |
| agent-linux-1 (002)  |       | agent-linux-2 (003)  |
| 10.0.1.237           |       | 10.0.1.177           |
+----------+-----------+       +----------+-----------+
           |                              |
           |           TCP 1514           |
           +---------------+--------------+
                           |
                           v
             +--------------------------+
             | Wazuh Manager            |
             | 10.0.1.80                |
             | Event analysis and rules |
             +-------------+------------+
                           ^
                           | TCP 1514
                           |
             +-------------+------------+
             | Windows Agent            |
             | Windows-EC2 (004)        |
             | 10.0.1.115               |
             +--------------------------+
```

```text

                      Wazuh Manager
                            |
                            | Filebeat forwards analyzed
                            | alert data to the Indexer
                            v
              +--------------------------+
              | Wazuh Indexer            |
              | Search and data storage  |
              +-------------+------------+
                            |
                            | Indexed data queries
                            v
              +--------------------------+
              | Wazuh Dashboard          |
              | HTTPS / TCP 443          |
              +--------------------------+
```

### Data Processing Stages

1. **Collection:** Each endpoint generates system and security events. Agents collect the data enabled in their configurations.
2. **Transmission:** Agents send events to the Wazuh Manager at `10.0.1.80` over TCP port `1514`.
3. **Analysis:** The Manager decodes the received events, evaluates them against Wazuh rules and generates alerts when applicable.
4. **Indexing:** Filebeat forwards alert data from the Wazuh server to the Indexer, which indexes and stores the data.
5. **Visualization:** The Dashboard queries the Indexer to display searchable security data and alerts.

## 6. Verification Notes and Recommendations

The following items should be checked periodically to keep the architecture documentation accurate:

- **Agent status:** Confirm all three agents appear as active in the Wazuh Dashboard.
- **Component services:** Check that `wazuh-manager`, `wazuh-indexer` and `wazuh-dashboard` are running on the Manager host.
- **Listening ports:** Verify that TCP ports `1514` and `1515` are listening when required by the configuration.
- **Dashboard access:** Confirm HTTPS access works from an authorized client.
- **Network access:** Review the AWS security group to ensure only required ports are open to authorized sources.

## 7. References

- [Wazuh Architecture](https://documentation.wazuh.com/current/getting-started/architecture.html)
- [Wazuh Agent Enrollment Requirements](https://documentation.wazuh.com/current/user-manual/agent/agent-enrollment/requirements.html)
- [Wazuh Agent Installation and Compatibility](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/index.html)