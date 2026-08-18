# RHEL-OS-Migration-Playbook
An Ansible Playbook for RHEL OS Upgrades utilizing Leapp. Created for EOL version 7->8, but can be used for future releases. Playbook also aims to tackle common inhibitors in a VMware vSphere environment, as well as pre deployment snapshots of all targeted machines within your inventory file. You must also have at least snapshot level permissions in vSphere to execute this playbook, as you will be using your account to make the call to vCenter to begin the snapshot process


Key Points to Note (Questions & Issues):
  - "Pin release to 7.9" will address any issues with subscription manager trying to talk to an 8.10 release on a 7.9 box (seen in environment).

  - This repo will only include the actual yml file to execute the OS upgrades. You will have to create your own directory in which the playbook will live, your own inventory file, and own vault file with ansible-vault encryption (unless you want to go plaintext, then have at it without the vault but I do not recommend that. Especially in today's landscape). Attached below will be the commands to run to set these up.
      ```bash
       mkdir -p /YOUR_PATH_HERE
       cd /YOUR_PATH_HERE
       touch inventory.ini # Hosts to upgrade will be stored in here
       vim inventory.ini
       touch vault.yml # vCenter credentials will be stored in here
       vim vault.yml # inside here YOUR_VCENTER_USERNAME & YOUR_VCENTER_PASSWORD
       ansible-vault encrypt vault.yml
      ```
  - Leapp inhibitors will be environmentally specific, there is no real way to tell what you might run into that'll stop the playbook in it's tracks until
    you let it fail. However, there are a few common inhibitors that I have seen that I have addressed in the playbook. These include:
  
    - pata_acpi <- Old kernel driver for IDE/PATA storage controllers.
    - Smartcard auth
    - Old kernel devels
    - NOTE: CIFS/Samba mounts will also produce high risk inhibitors. On target hosts, simply check /etc/fstab to verify none mounted and if they are, comment them out.
  
  - Prerequisites to run this playbook will include the installation of the following community modules
    - community.vmware
    - vmware.vmware
    - ansible.posix
    - community.general
    - community.library_inventory_filtering_v1
  - You will also need:
    - Ansible accounts with sudo access on each target machine
    - SSH key based auth, keys copied to each target machine for passwordless auth. ssh-keygen & ssh-copy-id are your friends.
  
   
  
