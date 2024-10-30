Ansible CLI Tools
=========
Ansible command line tools.

Downloading Ansible Automation Platform
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

- [Register system with Red Hat customer portal](https://access.redhat.com/solutions/253273 "RHSM")
- Run the following commands
```
sudo -i
dnf install ansible-core
git clone https://github.com/ericcames/ansible.cli.git

```
- Ensure that the correct checksum values are used in this variable: aap_sha_value for the distro you are planning to load
- [distributions.yml](https://github.com/ericcames/ansible.cli/blob/main/files/distributions.yml "distributions.yml")

**Create an ansible-vault file**

- Run the following command to create your vault.yml file:
```
ansible-vault create vault.yml
```
- Remember your vault password
- [Vaulted secrets.yml](https://github.com/ericcames/ansible.cli/blob/main/files/vault.yml "Vaulted")
- [Example secrets.yml](https://github.com/ericcames/ansible.cli/blob/main/files/example_vault.yml "Example")

**Now you are ready to run your playbook**

- The vault password is the password you used to create your vault
- Run the following command
```
ansible-playbook -i inventory setup.yml --ask-vault-pass
```
