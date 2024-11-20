Ansible CLI Tools
=========
Ansible command line tools.

Downloading Ansible Automation Platform
=========
This will download the software and setup an inventory file for 2.4 rpm, 2.4 containerized, 2.5 rpm, 2.5 containerized.  For the containerized version it creates the non root account (ansible-svc). You will need to validate that you have the correct checksum for the software that you are going to use.  You will be prompted with system checks before the automation proceeds.  Additionally all of your credentials will be vaulted so your CISO will love you.

![alt text](https://github.com/ericcames/ansible.cli/blob/main/images/CLIprompt.png "Prompt")

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
- [distributions.yml](https://github.com/ericcames/ansible.cli/blob/main/playbooks/files/distributions.yml "distributions.yml")

**Create an ansible-vault file**

- Run the following command to create your vault.yml file:
```
cd ansible.cli/playbooks/files
rm vault.yml
ansible-vault create vault.yml
```
Global Search and replace for vi
```
esc :%s/PASSWORD/newpassword/g

Also update registry user and password in the vault

# Always need our Red Hat Customer Portal creds to get our sofware
registry_username: MickeyMouse
registry_password: PASSWORD
```

- Remember your vault password
- [Vaulted secrets.yml](https://github.com/ericcames/ansible.cli/blob/main/playbooks/files/vault.yml "Vaulted")
- [Example secrets.yml](https://github.com/ericcames/ansible.cli/blob/main/playbooks/files/example_vault.yml "Example")

**If you are doing a containerized install update the public ssh key for the ansible-svc user with your public key**

- [ansible-svc](https://github.com/ericcames/ansible.cli/blob/main/playbooks/files/public_keys/ansible-svc "ansible-svc")

```
AWS
cat ~ec2-user/.ssh/authorized_keys >> ~root/ansible.cli/playbooks/files/public_keys/ansible-svc
```

**Now you are ready to prepare for the ansible platform install**

- The vault password is the password you used to create your vault
- Run the following command
```
cd ~/ansible.cli
ansible-playbook -i inventory playbooks/setup.yml --ask-vault-pass
```

**Time to install ansible automation platform**

Legacy Ansible Platform install command line with vaulted creds
```
cd ~/ansible-platform*
./setup.sh -i inventory -e@vault.yml -- --ask-vault-pass
```

- If you are using the containerized version logout and log back in as the ansible-svc user

Containerized Ansible Platform install command line with vaulted creds
```
cd ~/ansible-platform*
ansible-playbook -i inventory-growth ansible.containerized_installer.install -e@vault.yml --ask-vault-pass
```

**Keep your offline tokens from Red Hat alive**

- The Red Hat token will expire if it is not used every 30 days.
- [Token Keep Alive](https://github.com/ericcames/token.keepalive "Token Keep Alive ")