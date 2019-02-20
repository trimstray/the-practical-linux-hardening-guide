## Post install tasks

### Keep system updated

#### :information_source: Introduction

Software updates offer plenty of benefits. It’s all about revisions. These might include repairing security holes that have been discovered and fixing or removing bugs.

Some benefits:

- close up problems of security that has been discovered
- it can improve the stability of the system
- improvements the system stacks, e.g. network stack

#### :eight_pointed_black_star: Make sure that the system is up to date

###### RedHat/CentOS

```bash
# Check for updates
yum check-update

# Install updates
yum update

# Install upgrades (with security updates)
yum --security upgrade
```

###### Policy

| Type | Severity | Reference | Comment |
| :---         | :---         | :---         | :---       |
| <sup>OpenSCAP</sup> | <sup>High</sup> | <sup>[Ensure Software Patches Installed](https://static.open-scap.org/ssg-guides/ssg-centos7-guide-pci-dss.html#xccdf_org.ssgproject.content_rule_security_patches_up_to_date)<sup> | |
| <sup>STIG</sup> | <sup>Medium</sup> | <sup>[Vendor packaged system security patches and updates must be installed and up to date.](https://www.stigviewer.com/stig/red_hat_enterprise_linux_7/2017-12-14/finding/V-71999)</sup> | <sup>ID: V-71999</sup> |
| <sup>CIS</sup> | | | <sup>ID: 1.2, 1.8</sup> |

###### Debian

```bash
# Check for updates
apt-get update && apt-get upgrade

# Install updates
apt-get upgrade && apt-get dist-upgrade
```

#### :eight_pointed_black_star: Automatic security updates

###### RedHat/CentOS

```bash
yum install yum-cron

# Edit /etc/yum/yum-cron.conf
update_cmd = security
apply_updates = yes

# Enable service
systemctl enable yum-cron
systemctl start yum-cron
```

###### Debian

```bash
apt-get install unattended-upgrades apt-listchanges

# Edit /etc/apt/apt.conf.d/20auto-upgrades
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";
```

#### :eight_spoked_asterisk: Useful resources

- [How Often Should I Update our Linux Server?](https://serverfault.com/questions/9490/how-often-should-i-update-our-linux-server)

#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
| Regulary update your system | :black_square_button: | :black_square_button: |
| Automatic check system updates | :black_square_button: | :black_square_button: |
