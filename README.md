# ANSIBLE

# INVENTORY
```
Inventory is nothing but the collection of all hosts that you want to connect and configure.
```

# SAMPLE INVENTORY
**Example:**
```
[dev]
34.93.68.208
34.93.171.87
[control]
35.244.12.65 ansible_connection=local
```

# List all hosts
```ansible --list-host all```

**Exampple : ansible -i sample --list-hosts all**
 ```
  hosts (3):
    34.93.68.208
    34.93.171.87
    35.244.12.65
```

# Host Selection
```
We can select particular group of hosts using wildcard characters or by using the group name as input to --list-hosts command.
```
**Example 1: ansible --list-hosts all**
 ```
  hosts (3):
    34.93.68.208
    34.93.171.87
    35.244.12.65
```
**Example 2: ansible --list-hosts dev**
 ```
 This will list all the hosts which are in dev group
  hosts (2):
    34.93.68.208
    34.93.171.87
```
**Example 3: ansible --list-hosts all !dev**
 ```
 This will list all the hosts which are not in dev group.
  hosts (1):
    35.244.12.65
```
**Example 4: ansible --list-hosts dev[1]**
 ```
 This will list all the hosts which are in dev group
  hosts (1):
    34.93.171.87
```

# TASKS
# Simple adhoc tasks

```
ansible -m command -a "ls -la" dev
This is will execute the "ls -la" command on all the dev hosts mentioned in our inventory file.
```

# PLAYBOOKS
```
A playbook is file to execute a sequence of tasks on the hosts.
A playbook file is a YML file.
```

**Example: hostname.yml**
```
---
  - hosts: all
    tasks:
    - command: hostname
    - command: pwd
```
```ansible-playbook hostname.yml```
**Output**
```
PLAY [all] *************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************
ok: [34.93.171.87]
ok: [34.93.68.208]
ok: [35.244.12.65]

TASK [command] *********************************************************************************************************************
skipping: [35.244.12.65]
skipping: [34.93.171.87]
skipping: [34.93.68.208]

TASK [command] *********************************************************************************************************************
skipping: [35.244.12.65]
skipping: [34.93.68.208]
skipping: [34.93.171.87]

PLAY RECAP *************************************************************************************************************************
34.93.171.87               : ok=1    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
34.93.68.208               : ok=1    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
35.244.12.65               : ok=1    changed=0    unreachable=0    failed=0    skipped=2    rescued=0    ignored=0
```

**Let's see the how to install a ngnix package in all dev machines using ansible plabooks**

**Example: development.yml**
```
---
 - hosts: dev
   become: true
   tasks:
    - name: Install Nginx
      yum: 
        name: nginx
        state: present
        update_cache: true   
```
```
[dev_krishnasai@controller ansible]$ ansible-playbook development.yml
```
**Output**
```
PLAY [dev] ***************************************************************************************************************

TASK [Gathering Facts] ***************************************************************************************************
ok: [10.160.0.17]
ok: [10.160.0.18]

TASK [Install Nginx] *****************************************************************************************************
changed: [10.160.0.17]
changed: [10.160.0.18]

PLAY RECAP ***************************************************************************************************************
10.160.0.17                : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
10.160.0.18                : ok=2    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

# ANSIBLE FACTS
```
Ansible facts are the system properties collected by the ansible to when it executes on a managedhost or remote host.
These facts contains some useful details such as network configuration, ipv4, ipv6, storage information etc
```
**Examples:**
```
ansible all -m setup
```
```
This will give you the facts of dev nodes defined in your host configuration
```

