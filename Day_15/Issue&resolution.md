** Challenge  – Bastion Host Connectivity Failed**

* **Issue:** I tried to connect to an EC2 instance in a private subnet via a bastion host but SSH kept failing.
* **Root Cause:** The **security group** attached to the private instance didn’t have an **inbound rule allowing SSH (port 22)** from the bastion host.
* **Resolution:** Added a security group rule to allow port 22 from the **bastion host’s security group** → SSH worked successfully.





