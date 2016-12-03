# Discover network interface cards
ls /sys/class/net

# Edit /etc/network/interfaces and add p1p1 static IP
sudo nano /etc/network/interfaces

# Turn off Ansible host key checking
export ANSIBLE_HOST_KEY_CHECKING=False

# Execute playbook to prep OpenStack server
ansible-playbook -i hosts -k -K all.yml

*************************************************************************
Please pause here as we just rebooted the OpenStack server and it needs
to come back online.  OpenStack Trivia time!!!
Wait approximately 5 minutes before proceeding.
*************************************************************************

# Execute playbook to setup OSA deployment on OpenStack server
ansible-playbook -i hosts prep_deploy.yml

# SSH to OpenStack server
ssh <OpenStack Server IP> -l root

# Change into OSA playbooks directory
cd /opt/openstack-ansible

# Execute the following OSA playbooks (go grab some coffee, just kidding)
cd playbooks
openstack-ansible setup-everything.yml

# Open browser and connect to the OpenStack server IP (if nothing failed but, please smile even if it did)
https://<OpenStack Server IP>
