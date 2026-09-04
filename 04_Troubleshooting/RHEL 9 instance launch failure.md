# RHEL 9 instance launch failure

Error:
Volume of size 8GB is smaller than the required AMI snapshot

Cause:
The selected RHEL 9 AMI required a root volume of at least 10 GiB, while the instance had initially been configured with only 8 GiB.

Resolution:
The root EBS volume was increased from 8 GiB to 10 GiB. The instance was then successfully launched.

**Status: Resolved**