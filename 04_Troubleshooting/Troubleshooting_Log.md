# SOCWatch - Troubleshooting Log

**Project:** Wazuh SOC Monitoring Lab  
**Environment:** AWS EC2, Ubuntu, RHEL, Windows Server, Wazuh 4.14.7  
**Purpose:** Document the main technical issues encountered during deployment and configuration, along with their causes and resolutions.

---

## Issue 1: RHEL 9 Instance Launch Failure

**Problem:** The EC2 instance could not launch because the configured 8 GiB root volume was smaller than the minimum required by the selected AMI snapshot.

**Cause:** The selected RHEL 9 AMI required a root volume of at least 10 GiB.

**Resolution:** Increased the root EBS volume from 8 GiB to 10 GiB and relaunched the instance.

**Status:** Resolved

---

## Issue 2: Insufficient RAM for Wazuh Manager Installation

**Problem:** The initial Wazuh Manager instance, configured as `t3.small` with approximately 2 GiB of RAM, did not meet the installer's hardware requirements.

**Cause:** The instance had less memory than the installer expected.

**Resolution:** Deployed a new manager configuration as `c7i-flex.large` with approximately 3.7 GiB of RAM and used the installer's `-i` option to bypass its hardware check.

**Status:** Installation completed. 

---

## Issue 3: PuTTY Session Disconnection During Installation

**Problem:** The SSH session disconnected while Filebeat was being installed, interrupting visibility into the installation process.

**Cause:** The installation was running within a terminal session that could end when the SSH connection dropped.

**Resolution:** Used a `tmux` session for the subsequent installation so the process could continue independently of the SSH terminal connection.

**Status:** Resolved for the subsequent installation.

---

## Issue 4: Invalid XML Structure in the Windows Agent Configuration

**Problem:** The Windows Wazuh agent failed to validate its configuration and reported errors such as:

```text
ERROR: (1230): Invalid element in the configuration: 'wazuh_config'.
ERROR: (1215): No client configured. Exiting.
```

**Cause:** Changes to `ossec.conf` introduced multiple top level XML elements instead of keeping the configuration under one `<ossec_config>` root element.

**Resolution:** Replaced the malformed configuration with a single root XML structure and placed the required client settings inside it. The manager address was set to `10.0.1.80`, using TCP port `1514`.

**Status:** Configuration corrected. Confirm successful service startup and agent connectivity in the Wazuh Dashboard.

---

## Issue 5: Invalid `users` Setting in Windows Syscollector Configuration

**Problem:** The Windows agent reported configuration errors:

```text
ERROR: No such tag 'users' at module 'syscollector'.
ERROR: (1202): Configuration error at 'ossec.conf'.
```

**Cause:** The `<users>` element was not accepted in the configured `<syscollector>` section.

**Resolution:** Removed the unsupported element and retained the supported Syscollector configuration options.

**Status:** Configuration corrected. Verify that the agent starts without further configuration errors.

---

## Issue 6: Systemd Warning on the Linux Agent

**Problem:** Starting the Wazuh agent on `agent-linux-1` produced a warning that the service unit files had changed on disk.

**Cause:** Systemd's loaded service configuration was out of sync with the files on disk.

**Resolution:** Reloaded the systemd configuration and restarted the agent:

```bash
sudo systemctl daemon-reload
sudo systemctl restart wazuh-agent
```

**Status:** Resolved.

---

## Issue 7: Public IP Changes After EC2 Restart

**Problem:** Stopping and restarting EC2 instances can result in different public IP addresses when Elastic IPs are not configured.

**Impact:** Public IP changes may affect remote administration or services configured to depend on those addresses.

**Resolution / Design Decision:** Configured the agents to communicate with the Wazuh Manager using its private VPC address, `10.0.1.80`, over TCP port `1514`. This avoids depending on the manager's public IP for internal agent communication.

**Status:** Verify agent connectivity after restarting instances.

---

## Troubleshooting Summary

The main issues involved EC2 storage requirements, Wazuh installation resources, SSH session reliability, agent configuration syntax, systemd service management, and changing public IP addresses.

Resolving these issues helped establish a more reliable lab setup. Configuration changes and service restarts should always be followed by verification in the relevant service logs and the Wazuh Dashboard.