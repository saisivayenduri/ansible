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
```
**Output**
```
PLAY [all] *************************************************************************************************************************

TASK [Gathering Facts] *************************************************************************************************************
ok: [35.244.12.65]
ok: [34.93.68.208]
ok: [34.93.171.87]

TASK [command] *********************************************************************************************************************
skipping: [35.244.12.65]
skipping: [34.93.171.87]
skipping: [34.93.68.208]

PLAY RECAP *************************************************************************************************************************
34.93.171.87               : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
34.93.68.208               : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
35.244.12.65               : ok=1    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
```
