## Services

### Disable all unnecessary services

The action in this section provide guidance on some of unwanted applications and services which you might not needed but they are installed by default during OS installation and unknowingly start eating your system resources and also threats to the system security. If unused services is not enabled then it cannot be exploited.

#### :eight_pointed_black_star: Common Unix Print System

The Common Unix Print System (CUPS) provides the ability to print to both local and network printers. If the system does not need to accept print jobs from other systems, it's recommended that CUPS be disabled to reduce the potential attack.

Run the following command to verify cups is not enabled:

```bash
# systemctl is-enabled cups
disabled
```

Run the following command to disable cups:

```bash
# systemctl disable cups
```

###### Policies

- STIG:

- CIS:
