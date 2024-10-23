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

![alt text](https://github.com/ericcames/aap.dailydemo.F5/blob/main/images/F5joblog.png "Job Log")

```
https://ec2-54-67-87-75.us-west-1.compute.amazonaws.com:8443
```
# The command line; there's no place like home :-)

![alt text](https://github.com/ericcames/aap.dailydemo.F5/blob/main/images/F5cli.png "The command line")

Example login using your ssh key that was shared with Amazon
```
ssh admin@ec2-54-67-87-75.us-west-1.compute.amazonaws.com
```

**The playbook**

[1. Create and Delete F5](https://github.com/ericcames/aap.dailydemo.F5/blob/main/playbooks/main.yml "main.yml")<br>
![alt text](https://github.com/ericcames/aap.dailydemo.F5/blob/main/images/F5job.png "Create")<br>

Tags used:
```
create
  or
remove
```

**The Credentials Types**

Red Hat Ansible Automation Platform<br>
Daily Demo F5 Machine Credential<br>
![alt text](https://github.com/ericcames/aap.dailydemo.F5/blob/main/images/F5machinecred.png "Machine Credential")<br>
Amazon Web Services Credential<br>

**The AAP Managed Inventory**

![alt text](https://github.com/ericcames/aap.dailydemo.F5/blob/main/images/F5inventory.png "AAP Managed Inventory")<br>

Group name
```
f5demo
```

**The Cleanup Schedule**
![alt text](https://github.com/ericcames/aap.dailydemo.F5/blob/main/images/F5cleanup.png "F5 Daily Demo Cleanup")<br>
