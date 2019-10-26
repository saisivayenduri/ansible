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
```

# List all hosts
```ansible --list-host all```

**Exampple : ansible -i sample --list-hosts all**
 ```
  hosts (2):
    34.93.68.208
    34.93.171.87
```
