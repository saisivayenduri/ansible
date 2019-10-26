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
We can select particular group of hosts using wildcard characters or by using the group name as input to **--list-hosts** command
```
