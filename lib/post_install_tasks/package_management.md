## Post install tasks

### Package management

#### :information_source: Introduction

Package manager is a popular way to distribute software. It's also provide a privileged, central mechanism for the management of software on your operating system.

#### :eight_pointed_black_star: Check package signatures

###### RedHat/CentOS

```bash
# Edit '[main]' section in /etc/yum.conf
gpgcheck=1
```

###### Policy

| Type | Severity | Reference | Comment |
| :---         | :---         | :---         | :---       |
| <sup>OpenSCAP</sup> | <sup>High</sup> | <sup>[Ensure gpgcheck Enabled In Main yum Configuration ](https://static.open-scap.org/ssg-guides/ssg-centos7-guide-pci-dss.html#xccdf_org.ssgproject.content_rule_ensure_gpgcheck_globally_activated)<sup> | |
| <sup>STIG</sup> | <sup></sup> | <sup></sup> | <sup></sup> |
| <sup>CIS</sup> | | | <sup></sup> |

#### :eight_pointed_black_star: Remove packages with known issues

###### RedHat/CentOS

```bash

```

###### Policy

| Type | Severity | Reference | Comment |
| :---         | :---         | :---         | :---       |
| <sup>OpenSCAP</sup> | <sup></sup> | <sup><sup> | |
| <sup>STIG</sup> | <sup></sup> | <sup></sup> | <sup></sup> |
| <sup>CIS</sup> | | | <sup></sup> |

#### :eight_spoked_asterisk: Useful resources



#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
|  | :black_square_button: | :black_square_button: |
|  | :black_square_button: | :black_square_button: |
