# RHEL-OS-Migration-Playbook
An Ansible Playbook for RHEL OS Upgrades utilizing Leapp. Created for EOL version 7->8, but can be used for future releases. Playbook also aims to tackle common inhibitors in a VMware vSphere environment, as well as pre deployment snapshots of all targeted machines within your inventory file.


Key points to note:
  - "Pin release to 7.9" will address any issues with subscription manager trying to talk to an 8.10 release on a 7.9 box.
