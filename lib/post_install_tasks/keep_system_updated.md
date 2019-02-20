## Post install tasks

### Keep system updated

#### :information_source: Introduction

Software updates offer plenty of benefits. It’s all about revisions. These might include repairing security holes that have been discovered and fixing or removing computer bugs.

Some benefits:

- close up problems of security that has been discovered
- it can improve the stability of the system
- improvements the system stacks, e.g. network stack

#### :eight_pointed_black_star: Make sure that the system is up to date

For CentOS:

```bash
# Check for updates
yum check-update

# Install updates
yum update
```

For Debian:

```bash
# Check for updates
apt-get update -qq ; apt-get upgrade -duyq

# Install updates
apt-get upgrade && apt-get dist-upgrade
```

###### Useful resources

- [How Often Should I Update our Linux Server?](https://serverfault.com/questions/9490/how-often-should-i-update-our-linux-server)

###### Policies

| <b><u>Policy</u></b> | <b><u>ID/Description</u></b> | <b><u>Severity</u></b> |
| :---         | :---         | |
| <b>STIG</b> | [V-71999](https://www.stigviewer.com/stig/red_hat_enterprise_linux_7/2017-12-14/finding/V-71999) | Severity: <b>Medium</b> |
| <b>CIS</b> | 1.2, 1.8 | |
| <b>OpenSCAP</b> | CCI-002605, CCI-002607 | CAT II |

#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
| Regulary update your system | :black_square_button: | :black_square_button: |
| Automatic check system updates | :black_square_button: | :black_square_button: |
