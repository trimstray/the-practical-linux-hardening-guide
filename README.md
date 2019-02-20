<h2 align="center"><code>The Practical Linux Hardening Guide</code></h2>

<br>

<p align="center">
    <img src="https://github.com/trimstray/the-practical-linux-hardening-guide/blob/master/doc/img/main_preview.jpg"
        alt="Master">
</p>

<br>

<p align="center">"<i>Did you know all your doors were locked?</i>" - Riddick (The Chronicles of Riddick)</p>

<br>

<p align="center">
  <a href="https://github.com/trimstray/the-practical-linux-hardening-guide/tree/master">
    <img src="https://img.shields.io/badge/Branch-master-green.svg?longCache=true"
        alt="Branch">
  </a>
  <a href="https://github.com/trimstray/the-practical-linux-hardening-guide/pulls">
    <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg?longCache=true"
        alt="Pull Requests">
  </a>
  <a href="http://www.gnu.org/licenses/">
    <img src="https://img.shields.io/badge/License-GNU-blue.svg?longCache=true"
        alt="License">
  </a>
</p>

<div align="center">
  <sub>Created by
  <a href="https://twitter.com/trimstray">trimstray</a> and
  <a href="https://github.com/trimstray/the-practical-linux-hardening-guide/graphs/contributors">
    contributors
  </a>
</div>

<br>

<p align="center"><code>I'm back, work in progress...</code>

****

## Table of Contents

- **[Introduction](#introduction)**
  * [General disclaimer](#general-disclaimer)
  * [The importance of Linux hardening](#the-importance-of-linux-hardening)
  * [How to hardening Linux?](#how-to-hardening-linux)
  * [Which distribution should be used?](#which-distribution-should-be-used)
  * [How to read this guide?](#how-to-read-this-guide)
  * [Okay. Let's start, 3, 2, 1... STOP!](#okay-let-s-start-3-2-1-stop)
- **[Policy Compliance](#policy-compliance)**
  * [Center of Internet Security (CIS)](#center-of-internet-security-cis)
  * [Security Technical Implementation Guide (STIG)](#security-technical-implementation-guide-stig)
  * [National Institute of Standards and Technology (NIST)](#national-institute-of-standards-and-technology-nist)
  * [Payment Card Industry Data Security Standard (PCI-DSS)](#payment-card-industry-data-security-standard-pci-dss)
- **[Security Content Automation Protocol (SCAP)](#security-content-automation-protocol-scap)**
  * [SCAP Security Guide](#scap-security-guide)
  * [OpenSCAP Base](#openscap-base)
  * [SCAP Workbench](#scap-workbench)
- **[DevSec Hardening Framework](#devsec-hardening-framework)**
- **[Contributing & Support](#contributing--support)**
- **[License](#license)**
- **[External resources](#external-resources)**
  * [Other official hardening guides](lib/external_resources/other_official_hardening_guides.md#other-official-hardening-guides)
- **[Pre install tasks](#pre-install-tasks)**
  * **[Physical system security](lib/pre_install_tasks/physical_system_security.md#physical-system-security)**
    + [Introduction](lib/pre_install_tasks/physical_system_security.md#information_source-introduction)
    + [Secure rooms](lib/pre_install_tasks/physical_system_security.md#eight_pointed_black_star-secure-rooms)
    + [Monitoring](lib/pre_install_tasks/physical_system_security.md#eight_pointed_black_star-monitoring)
    + [Air conditioning](lib/pre_install_tasks/physical_system_security.md#eight_pointed_black_star-air-conditioning)
    + [Fire protection](lib/pre_install_tasks/physical_system_security.md#eight_pointed_black_star-fire-protection)
    + [Locked racks](lib/pre_install_tasks/physical_system_security.md#eight_pointed_black_star-locked-racks)
    + [Console security](lib/pre_install_tasks/physical_system_security.md#eight_pointed_black_star-console-security)
    + [BIOS protection](lib/pre_install_tasks/physical_system_security.md#eight_pointed_black_star-bios-protection)
    + [Summary checklist](lib/pre_install_tasks/physical_system_security.md#ballot_box_with_check-summary-checklist)
  * **[Hard disk encryption](lib/pre_install_tasks/hard_disk_encryption.md#hard-disk-encryption)**
    + [Introduction](lib/pre_install_tasks/hard_disk_encryption.md#information_source-introduction)
    + [Encrypt root filesystem](lib/pre_install_tasks/hard_disk_encryption.md#eight_pointed_black_star-encrypt-root-filesystem)
    + [Encrypt /boot partition](lib/pre_install_tasks/hard_disk_encryption.md#eight_pointed_black_star-encrypt-boot-partition)
    + [Swap partition](lib/pre_install_tasks/hard_disk_encryption.md#eight_pointed_black_star-swap-partition)
    + [Summary checklist](lib/pre_install_tasks/hard_disk_encryption.md#ballot_box_with_check-summary-checklist)
- **[Post install tasks](#post-install-tasks)**
  * **[Bootloader configuration (grub)](lib/post_install_tasks/bootloader_configuration.md#bootloader-configuration-grub)**
    + [Introduction](lib/post_install_tasks/bootloader_configuration.md#information_source-introduction)
    + [Protect bootloader with password](lib/post_install_tasks/bootloader_configuration.md#eight_pointed_black_star-protect-bootloader-with-password)
    + [Protect bootloader config files](lib/post_install_tasks/bootloader_configuration.md#eight_pointed_black_star-protect-bootloader-config-files)
    + [Summary checklist](lib/post_install_tasks/bootloader_configuration.md#ballot_box_with_check-summary-checklist)
  * **[Disk partitions](lib/post_install_tasks/disk_partitions.md#disk-partitions)**
    + [Introduction](lib/post_install_tasks/disk_partitions.md#information_source-introduction)
    + [Separate disk partitions](lib/post_install_tasks/disk_partitions.md#eight_pointed_black_star-separate-disk-partitions)
    + [Mount options: nodev, noexec and nosuid](lib/post_install_tasks/disk_partitions.md#eight_pointed_black_star-mount-options-nodev-nosuid-and-noexec)
    + [Secure /boot directory](lib/post_install_tasks/disk_partitions.md#eight_pointed_black_star-secure-boot-directory)
    + [Secure /tmp and /var/tmp](lib/post_install_tasks/disk_partitions.md#eight_pointed_black_star-secure-tmp-and-vartmp)
    + [Secure /dev/shm](lib/post_install_tasks/disk_partitions.md#eight_pointed_black_star-secure-devshm)
    + [Secure /proc filesystem](lib/post_install_tasks/disk_partitions.md#eight_pointed_black_star-secure-proc-filesystem)
    + [Swap partition](lib/post_install_tasks/disk_partitions.md#eight_pointed_black_star-swap-partition)
    + [Disk quotas](lib/post_install_tasks/disk_partitions.md#eight_pointed_black_star-disk-quotas)
    + [Summary checklist](lib/post_install_tasks/disk_partitions.md#ballot_box_with_check-summary-checklist)
  * **[Keep system updated](lib/post_install_tasks/keep_system_updated.md#keep-system-updated)**
    + [Introduction](lib/post_install_tasks/keep_system_updated.md#information_source-introduction)
    + [Make sure that the system is up to date](lib/post_install_tasks/keep_system_updated.md#eight_pointed_black_star-make-sure-that-the-system-is-up-to-date)
    + [Automatic security updates](lib/post_install_tasks/keep_system_updated.md#eight_pointed_black_star-automatic-security-updates)
    + [Useful resources](lib/post_install_tasks/keep_system_updated.md#link-useful-resource)
    + [Summary checklist](lib/post_install_tasks/keep_system_updated.md#ballot_box_with_check-summary-checklist)
  * **[Package management](#package-management)**
    + [Introduction](lib/post_install_tasks/package_management.md#information_source-introduction)
    + [Check package signatures](lib/post_install_tasks/package_management.md#information_source-introduction)
    + [Remove packages with known issues](lib/post_install_tasks/package_management.md#remove-packages-with-known-issues)
    + [Useful resources](lib/post_install_tasks/package_management.md#link-useful-resource)
    + [Summary checklist](lib/post_install_tasks/package_management.md#ballot_box_with_check-summary-checklist)
  * **[Netfilter ruleset](#netfilter-ruleset)**
    + [Shorewall](#shorewall)
  * **[TCP wrapper](#tcp-wrapper)**
  * **[Users and groups](#users-and-groups)**
    + [Limit su access](#limit-su-access)
    + [Disable root account](#disable-root-account)
    + [Logins to system console](#logins-to-system-console)
    + [Disable shell accounts](#disable-shell-accounts)
    + [Strong password policy](#strong-password-policy)
    + [Password aging](#password-aging)
    + [Previous passwords](#previous-passwords)
    + [Login failures](#login-failures)
    + [Protect single user mode](#protect-single-user-mode)
  * **[System path permissions](#system-path-permissions)**
    + [World writable files](#world-writable-files)
  * **[PAM module](#pam-module)**
  * **[Limits](#limits)**
  * **[Shadow passwords](#shadow-passwords)**
  * **[Linux kernel hardening](#linux-kernel-hardening)**
    + [Kernel parameters](#kernel-parameters)
      + [Network security](#improve-network-security)
      + [System security](#improve-system-security)
  * **[Remove unused modules](#remove-unused-modules)**
  * **[Secure shared memory](#secure-shared-memory)**
  * **[IRQ balance](#irq-balance)**
  * **[Disable compilers](#disable-compilers)**
  * **[Email notifications](#email-notifications)**
    + [Rebooting the system](#rebooting-the-system)
    + [Login the system](#login-the-system)
  * **[Backups](#backups)**
    + [Backup policy](#backup-policy)
  * **[External devices](#external-devices)**
    + [Disable USB usage](#disable-usb-usage)
- **[Tools](#tools)**
  * **[Logging and Auditing](#logging-and-auditing)**
    + [Syslog](#syslog)
    + [Auditd](#auditd)
    + [OSSEC](#ossec)
    + [Tiger](#tiger)
    + [Aide](#aide)
    + [Logwatch](#logwatch)
  * **[SELinux](#selinux)**
  * **[Other](#other)**
    + [Fail2ban](#fail2ban)
    + [PSAD](#psad)
    + [Entropy daemon](#entropy-daemon)
    + [Centralized authentication service](#centralized-authentication-service)
  * **[Testing tools](#testing-tools)**
    + [Lynis](#lynis)
    + [Chrootkit](#chrootkit)
- **[Services](#services)**
  * **[Disable all unnecessary services](lib/services/disable_all_unnecessary_services.md#disable-all-unnecessary-services)**
    + [Common unix print system](lib/services/disable_all_unnecessary_services.md#eight_pointed_black_star-common-unix-print-system)
    + [Summary checklist](lib/services/disable_all_unnecessary_services.md#ballot_box_with_check-summary-checklist)
  * **[System services](#system-services)**
    + [OpenSSH](#openssh)
    + [NTP](#ntp)
    + [Cron](#cron)
    + [Anacron](#anacron)
    + [GnuPG 2](#gnupg2)
      + [Unattended key generation](#unattended-key-generation)
  * **[DNS services](#dns-services)**
    + [Bind9](#bind9)
    + [Unbound](#unbound)
    + [Knot Resolver](#knot-resolver)
  * **[Mail services](#mail-services)**
    + [Postfix](#postfix)
  * **[Web services](lib/services/web_services.md#web-services)**
    + [Nginx](lib/services/web_services.md#nginx)
      - [Files and directories permissions](lib/services/web_services.md#eight_pointed_black_star-files-and-directories-permissions)
      - [Use HTTPS](lib/services/web_services.md#eight_pointed_black_star-use-https)
      - [Enable HTTP2](lib/services/web_services.md#eight_pointed_black_star-enable-http2)
      - [Separate domains](lib/services/web_services.md#eight_pointed_black_star-separate-domains)
      - [Redirect all unencrypted traffic to HTTPS](lib/services/web_services.md#eight_pointed_black_star-redirect-all-unencrypted-traffic-to-https)
      - [Enable HTTP Strict Transport Security](lib/services/web_services.md#eight_pointed_black_star-enable-http-strict-transport-security)
      - [Diffie Hellman Ephemeral Parameter](lib/services/web_services.md#eight_pointed_black_star-diffie-hellman-ephemeral-parameter)
      - [Security related headers](lib/services/web_services.md#eight_pointed_black_star-security-related-headers)
    + [Apache](#apache)
  * **[Databases](#databases)**
    + [PostgreSQL](#postgresql)
    + [MySQL](#mysql)
    + [Redis](#redis)
  * **[Queues](#queues)**
    + [AMQP](#amqp)
- **[Containers](#containers)**
  * **[LXC/LXD](#lxc-lxd)**
  * **[Docker](#docker)**
  * **[Hashicorp suite](#hashicorp-suite)**
- **[Deployment](#deployment)**
- **[Testing configuration](#testing-configuration)**

## Introduction

### General disclaimer

**The Practical Linux Hardening Guide** provides a high-level overview of the hardening GNU/Linux systems. It is not an official standard or handbook but it _touches_ and _use_ industry standards.

This guide also provides you with _practical step-by-step instructions_ for building your own hardened systems and services.

A few simple rules for this project:

- this guide is compliant with [OpenSCAP](https://www.open-scap.org/) (PCI-DSS)
- is based on a minimal [RHEL](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux) and [CentOS](https://www.centos.org/) installations
- it does not exhaust everything about Linux hardening
- it also contains non-related rules with PCI-DSS
- some hardening rules/descriptions can be done better
- you can think of it also as a checklist

Before you start remember:

  > This guide also contains my comments that may be differ from certain industry principles. If you are not sure what to do please see **[Policy Compliance](#policy-compliance)** chapter.

### The importance of Linux hardening

Simply speaking, hardening is the process of making a system more secure. Out of the box, Linux servers don’t come "hardened" (e.g. with the attack surface minimized). It’s up to you to prepare for each eventuality and set up systems to notify you of any suspicious activity in the future.

The process of hardening servers involves both IT ops. and security teams and require changes to the default configuration according to industry benchmarks.

You need to harden your system to protect your assets as much as possible. Why it's important? Please read a great and short article that [explains hardening process](https://linux-audit.com/linux-server-hardening-most-important-steps-to-secure-systems/) step by step by [Michael Boelen](https://michaelboelen.com/).

### How to hardening Linux?

In my opinion you should definitely drop all non-industry policies, articles, manuals and other (especially on your production environments but also if you harden standalone home server). These lists exist to give false sense of security and they are not bases on authority standards.

We have a lot of great GNU/Linux hardening policies to provide safer operating systems compatible with security protocols. For me, **CIS** and the **PCI-DSS** compliant are about the best actual prescriptive guides.

  > Most of all you should use [Security Benchmarks/Policies](#policy-compliance) which describe consensus best practices for the secure configuration of target systems because configuring your systems in compliance eliminate the most common security fails/bugs. For example, CIS has been shown to eliminate 80-95% of known security vulnerabilities.

On the other hand e.g. STIG itself is just a complicated (for newbies difficult to implement) check-list. In my opinion ideally, real world implementation is automated via something like OpenSCAP.

  > You should use a rational approach, remember that more is not better. Each environment is different so security rules should all work in theory, but sometimes it not works as well.

### Which distribution should be used?

This guide is being written and tested on **Red Hat Enterprise Linux** and **CentOS Linux** distributions because:

- they are a free (CentOS) and open source
- they are enterprise-class
- they are stable and reliable
- they have great community support
- they are built on coherent snapshots of old packages

Both distributions provides **[certified tools](#scap-security-guide)** which can parse and evaluate each component of the SCAP standard.

### How to read this guide?

The three levels of understanding:

- read the _main chapters_ (introduction and other sub chapters), e.g. _Linux kernel hardening_, it offers a general overview
- check the _useful resources_ for a deeper understanding
- check the _policies_ and on this basis, make changes

### Okay. Let's start, 3, 2, 1... STOP!

Making major changes to the direction of your systems can be risky.

The most important rule of system hardening that reasonable admins actually use is:

  > **`A production environment is the real instance of the app so all your changes make on the dev/test!`**

The second important rule is:

  > **`Don’t do anything that will affect the availability of the service or your system.`**

The third rule is:

  > **`Make backup of entire virtual machines and important components in the middle of them.`**

And the last rule is:

  > **`Think about what you actually do at your server.`**

## Policy Compliance

### Center of Internet Security (CIS)

The Center of Internet Security (CIS) is a nonprofit organization focused on improving public and private-sector cybersecurity readiness and response.

Please see **[CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks/)**.

### Security Technical Implementation Guide (STIG)

A Security Technical Implementation Guide (STIG) is a cybersecurity methodology for standardizing security protocols within networks, servers, computers, and logical designs to enhance overall security.

Please see **[Stigviewer](https://www.stigviewer.com/stigs)** for explore all stigs.

### National Institute of Standards and Technology (NIST)

A National Institute of Standards and Technology (NIST) is a physical sciences laboratory, and a non-regulatory agency of the United States Department of Commerce.

Please see **[National Checklist Program (NCP)](https://nvd.nist.gov/ncp/repository)**.

### Payment Card Industry Data Security Standard (PCI-DSS)

Payment Card Industry Data Security Standard (PCI-DSS) compliance is a requirement for any business that stores, processes, or transmits cardholder data.

In accordance with PCI-DSS requirements established a formal policy and supporting procedures for developing configuration standards for system components that are consistent with industry-accepted hardening standards like:

- Center of Internet Security (CIS)
- International Organization for Standardization (ISO)
- SysAdmin, Audit, Network, and Security (SANS) Institute
- National Institute of Standards and Technology (NIST)

## Security Content Automation Protocol (SCAP)

Security Content Automation Protocol (SCAP) provides a mechanism to check configurations, vulnerability management and evaluate policy compliance for a variety of systems.

One of the most popular implementations of SCAP is OpenSCAP and it is very helpful for vulnerability assessment and also as hardening helper.

Please see **[SCAP Security Policies](https://www.open-scap.org/security-policies/)**, **[OpenSCAP User Manual](https://static.open-scap.org/openscap-1.2/oscap_user_manual.html)** and **[OpenSCAP Static](https://static.open-scap.org/)**.

### SCAP Security Guide

The auditing system settings with SCAP Security Guide project contains guidance for settings of Red Hat/CentOS and it's validated by NIST.

You should inspect the security content of your system with `oscap info` module:

```bash
oscap info /usr/share/xml/scap/ssg/rhel7/ssg-rhel7-ds.xml
```

### OpenSCAP Base

The `oscap` tool scans your system, validate security compliance content and generate reports and guides based on these scans.

Official [OpenSCAP Base](https://www.open-scap.org/tools/openscap-base/) documentation say:

  > _The command-line tool, called `oscap`, offers a multi-purpose tool designed to format content into documents or scan the system based on this content. Whether you want to evaluate DISA STIGs, NIST‘s USGCB, or Red Hat’s Security Response Team’s content, all are supported by OpenSCAP._

Before use please see **[Using OSCAP](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/sect-using_oscap)** documentation.

```bash
# Installation:
yum install openscap-scanner

# Make a RHEL7 machine PCI-DSS compliant:
oscap xccdf eval --report report.html --profile xccdf_org.ssgproject.content_profile_pci-dss /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml

# Make a CentOS machine PCI-DSS compliant:
oscap xccdf eval --report report.html --profile xccdf_org.ssgproject.content_profile_pci-dss /usr/share/xml/scap/ssg/content/ssg-centos7-ds.xml
```

### SCAP Workbench

SCAP Workbench is a utility that offers an easy way to perform common `oscap` tasks on local or remote systems.

Before use please see **[Using SCAP Workbench](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/sect-using_scap_workbench)** documentation.

```bash
# Installation:
yum install scap-security-guide scap-workbench
```

## DevSec Hardening Framework

  > _Security + DevOps: Automatic Server Hardening._

This project covered some of the things in this guide, which can be automated (e.g. setting of grub password or enforcing the permissions of the common directories). It's a good start if you want to make some changes and see how it works from the level of automation tools.

Project: **[DevSec Hardening Framework](https://dev-sec.io)** + GH repository: **[dev-sec](https://github.com/dev-sec/)**.

Thanks for [@artem-sidorenko](https://github.com/artem-sidorenko)!

## Contributing & Support

If you find something which doesn't make sense, or one of these doesn't seem right, or something seems really stupid; please make a pull request or please add valid and well-reasoned opinions about your changes or comments.

Before add pull request please see **[this](CONTRIBUTING.md)**.

If this project is useful and important for you or if you really like _The Practical Linux Hardening Guide_, you can bring me **more positive energy**, give me some **good words** or **support this project** more. Thank you!

## License

GPLv3 : <http://www.gnu.org/licenses/>, for more please see [LICENSE](https://github.com/trimstray/the-practical-linux-hardening-guide/blob/master/LICENSE.md).
