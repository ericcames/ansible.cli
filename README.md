Ansible CLI Tools
=========
Ansible command line tools.

Downloading Ansible Autmation Platform
=========

**Generate an offline token from Red Hat**

- Login with your account that gives you access to ansible platform software.
- [Generate Token](https://gitlab.com/mlowcher/F5_examples "Generate Token")
- Click on the Generate Token button and make a note of your offline token.

![alt text](https://github.com/ericcames/aap.dailydemo.F5/blob/main/images/F5uipre.png "Pre Login")
![alt text](https://github.com/ericcames/aap.dailydemo.F5/blob/main/images/F5uipost.png "Post Login")

**The job logs contain the URL needed to login to the gui**
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

Day 2
=========

**Example Playbooks**
- [F5 example playbooks](https://gitlab.com/mlowcher/F5_examples "F5 example playbooks")


**Execution Environment**<br>
- [F5_ee](https://quay.io/locust61/f5_ee:0.1 "F5 Execution Environment")
```
quay.io/locust61/f5_ee:0.1
```
f5-execution-environment.yml
```
---
version: 3

images:
  base_image:
    name: registry.redhat.io/ansible-automation-platform-24/ee-minimal-rhel8:latest

dependencies:
  galaxy:
    collections:
      - f5networks.f5_modules
      - f5networks.f5_bigip
      - ansible.netcommon
  system:
    - pkgconf-pkg-config [platform:rpm]
    - systemd-devel [platform:rpm]
    - gcc [platform:rpm]
    - python39-devel [platform:rpm]
  python:
    - packaging
    - requests[security]
    - xmltodict
    - msgraph-sdk==1.0.0
    - psycopg2-binary
    - urllib3==1.26.15
options:
  package_manager_path: /usr/bin/microdnf
```

**A Network Credential is reguired for Day 2 ops**

![alt text](https://github.com/ericcames/aap.dailydemo.F5/blob/main/images/F5networkcred.png "Daily Demo F5 Network credential")<br>


# Looking for the Windows Daily Demo?

- [AAP Daily Demo Windows](https://github.com/ericcames/aap.dailydemo.windows "AAP Daily Demo Windows")

# Looking for the Linux Daily Demo?

- [AAP Daily Demo Linux](https://github.com/ericcames/aap.dailydemo.linux "AAP Daily Demo Linux")
