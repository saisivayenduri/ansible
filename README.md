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
# Simple tasks

```ansible -m command -a "ls -la" dev```

