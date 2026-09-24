# Issue 1 - RHEL 9 instance launch failure

Error:
Volume of size 8GB is smaller than the required AMI snapshot

Cause:
The selected RHEL 9 AMI required a root volume of at least 10 GiB, while the instance had initially been configured with only 8 GiB.

Resolution:
The root EBS volume was increased from 8 GiB to 10 GiB. The instance was then successfully launched.

**Status: Resolved**


# Issue 2 — Old manager insufficient RAM

The first manager was a t3.small with approximately 2 GB RAM. The Wazuh installer stopped with the hardware requirement error.

Resolution:

A new EC2 manager configuration was deployed with approximately 3.7 GiB RAM. The Wazuh installation was then completed using the -i option to bypass the installer's hardware check.

**Status: Resolved**


# Issue 3 — PuTTY disconnection

The first installation was interrupted from the user's perspective when the PuTTY session disconnected during Filebeat installation.

Resolution:

A tmux session was used for the new installation so the installation process could continue independently of the SSH terminal connection.

**Status: Resolved**