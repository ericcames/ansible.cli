Ansible CLI Tools
=========
Ansible command line tools.

Downloading Ansible Autmation Platform
=========

**Generate an offline token from Red Hat**

- Login with your account that gives you access to ansible platform software.
- [Generate Token](https://access.redhat.com/management/api "Generate Token")
- Click on the Generate Token button and make a note of your offline token.

![alt text](https://github.com/ericcames/ansible.cli/blob/main/images/CLItoken.png "Generate Token")


**Get the sha value for the software you want**

- [Download Red Hat Ansible Automation Platform](https://access.redhat.com/downloads/content/480/ver=2.4/rhel---9/2.4/x86_64/product-software "Download Red Hat Ansible Automation Platform")
- Select the correct version and architecture
  - This example 2.4 RHEL 9 x86_64
- Get the Checksum for “Ansible Automation Platform 2.4 Setup Bundle”
  - 21c0a27c809c1a98402bdb7605b67b62174b2f54155bad4146c1824be0830f70

![alt text](https://github.com/ericcames/ansible.cli/blob/main/images/CLIsha.png "Checksum")

**Login to the server that we will be running the Ansible installer from**

- [Register system with Red Hat customer protal](https://access.redhat.com/solutions/253273 "RHSM")
- Run the following commands
```
sudo -i
dnf install ansible-core
mkdir -pv ansible/playbooks
cd ansible/playbooks
vi download_software.yml
```
- Ensure that the correct checksum value is used in this variable: aap_bundle_sha_value
- [download_software.yml](https://github.com/ericcames/ansible.cli/blob/main/playbooks/download_software.yml "download_software.yml")

**Create and inventory file**

- [inventory](https://github.com/ericcames/ansible.cli/blob/main/playbooks/inventory "inventory")
```
echo localhost > inventory
```

**Create an ansible-vault file**

**Now you are ready to run your playbook**

- The vault password is the password you used to create your vault
- Run the following command
```
ansible-playbook -i inventory download_software.yml --ask-vault-pass
```