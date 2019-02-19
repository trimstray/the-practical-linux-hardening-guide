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
- **[Policy Compliance (Hardening standards)](#policy-compliance-hardening-standards)**
  * [Center of Internet Security (CIS)](#center-of-internet-security-cis)
  * [Security Technical Implementation Guide (STIG)](#security-technical-implementation-guide-stig)
  * [Security Content Automation Protocol (SCAP)](#security-content-automation-protocol-scap)
- **[DevSec Hardening Framework](#devsec-hardening-framework)**
- **[Contributing](#contributing)**
- **[Other hardening guides](#other-hardening-guides)**
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
  * **[Keep system updated](#keep-system-updated)**
  * [Package management](#package-management)
    + [Automatic security updates](#automatic-security-updates)
    + [Remove packages with known issues](#remove-packages-with-known-issues)
  * [Netfilter ruleset](#netfilter-ruleset)
  * [TCP wrapper](#tcp-wrapper)
  * [Users and groups](#users-and-groups)
    + [Limit su access](#limit-su-access)
    + [Disable root account](#disable-root-account)
    + [Logins to system console](#logins-to-system-console)
    + [Disable shell accounts](#disable-shell-accounts)
    + [Strong password policy](#strong-password-policy)
    + [Password aging](#password-aging)
    + [Previous passwords](#previous-passwords)
    + [Login failures](#login-failures)
    + [Protect single user mode](#protect-single-user-mode)
  * [System path permissions](#system-path-permissions)
    + [World writable files](#world-writable-files)
  * [PAM module](#pam-module)
  * [Limits](#limits)
  * [Shadow passwords](#shadow-passwords)
  * [Linux kernel hardening](#linux-kernel-hardening)
    + [Kernel parameters](#kernel-parameters)
      + [Network security](#improve-network-security)
      + [System security](#improve-system-security)
  * [Remove unused modules](#remove-unused-modules)
  * [Secure shared memory](#secure-shared-memory)
  * [IRQ balance](#irq-balance)
  * [Disable compilers](#disable-compilers)
  * [Email notifications](#email-notifications)
    + [Rebooting the system](#rebooting-the-system)
  * [Backups](#backups)
  * [External devices](#external-devices)
    + [Disable USB usage](#disable-usb-usage)
- **[Tools](#tools)**
  * [Logging and Auditing](#logging-and-auditing)
    + [Auditd](#auditd)
    + [Tiger](#tiger)
    + [Aide](#aide)
    + [Logwatch](#logwatch)
  * [Other](#other)
    + [Fail2ban](#fail2ban)
    + [PSAD](#psad)
    + [SELinux](#selinux)
    + [Entropy daemon](#entropy-daemon)
    + [Centralized authentication service](#centralized-authentication-service)
  * [Testing tools](#testing-tools)
    + [Lynis](#lynis)
    + [Chrootkit](#chrootkit)
- **[Services](#services)**
  * **[Disable all unnecessary services](lib/services/disable_all_unnecessary_services.md#disable-all-unnecessary-services)**
    + [Common unix print system](lib/services/disable_all_unnecessary_services.md#eight_pointed_black_star-common-unix-print-system)
    + [Summary checklist](lib/services/disable_all_unnecessary_services.md#ballot_box_with_check-summary-checklist)
  * [System services](#system-services)
    + [OpenSSH](#openssh)
    + [NTP](#ntp)
    + [Cron](#cron)
    + [Anacron](#anacron)
    + [GnuPG 2](#gnupg2)
      + [Unattended key generation](#unattended-key-generation)
  * [DNS services](#dns-services)
    + [Bind9](#bind9)
  * [Mail services](#mail-services)
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
  * [Databases](#databases)
    + [PostgreSQL](#postgresql)
    + [MySQL](#mysql)
    + [Redis](#redis)
  * [Queues](#queues)
    + [AMQP](#amqp)
- **[Containers](#containers)**
  * [LXC/LXD](#lxc-lxd)
  * [Docker](#docker)
  * [Hashicorp suite](#hashicorp-suite)
- **[Deployment](#deployment)**
- **[Testing configuration](#testing-configuration)**
- **[External resources](#external-resources)**

## Introduction

This Hardening Guide provide a high-level overview of the security hardening GNU/Linux systems.

## Policy Compliance (Hardening standards)

### Center of Internet Security (CIS)

The [Center for Internet Security (CIS)](https://www.cisecurity.org/cis-benchmarks/) is a nonprofit organization focused on improving public- and private-sector cybersecurity readiness and response.

### Security Technical Implementation Guide (STIG)

A [Security Technical Implementation Guide (STIG)]((https://www.stigviewer.com/stigs)) is a cybersecurity methodology for standardizing security protocols within networks, servers, computers, and logical designs to enhance overall security.

### Security Content Automation Protocol (SCAP)

Security Content Automation Protocol (SCAP) provides a mechanism to check configurations, vulnerability management and evaluate policy compliance for a variety of systems. One of the most popular implementations of SCAP is [OpenSCAP](https://www.open-scap.org/security-policies/) and it is very helpful for vulnerability assessment and also as hardening helper.

## DevSec Hardening Framework

  > _Security + DevOps: Automatic Server Hardening._

This project covered a lot of the things in this guide, which can be automated (e.g. setting of grub password or enforcing the permissions of the common directories).

Project: **[DevSec Hardening Framework](https://dev-sec.io)** + GH repository: **[dev-sec](https://github.com/dev-sec/)**.

Thanks for **[@artem-sidorenko](https://github.com/artem-sidorenko)**!

## Contributing

If you find something which doesn't make sense, or one of these doesn't seem right, or something seems really stupid; please make a pull request or please add valid and well-reasoned opinions about your changes or comments.

Before add pull request please see **[this](CONTRIBUTING.md)**.

## Other hardening guides

| <b><u>Type of list</u></b> | <b><u>Comment</u></b> |
| :---         | :---         |
| <b>[STIGs Master List](https://iase.disa.mil/stigs/Pages/a-z.aspx)</b> ||
| <b>[Arch Linux](https://wiki.archlinux.org/index.php/Security)</b> ||
| <b>[CentOS Linux](https://wiki.centos.org/HowTos/OS_Protection)</b> ||
| <b>[Debian GNU/Linux](https://www.debian.org/doc/manuals/securing-debian-howto/index.en.html)</b> | <sup>old guide - to update</sup> |
| <b>[Fedora Linux](https://docs.fedoraproject.org/en-US/Fedora/19/html/Security_Guide/index.html)</b> | <sup>old guide - to update</sup>  |
| <b>[Red Hat Enterprise](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/)</b> ||
| <b>[Slackware Linux](https://docs.slackware.com/howtos:security:start)</b> | <sup>some data may not be available</sup>  |
| <b>[Ubuntu Linux](https://help.ubuntu.com/lts/serverguide/security.html.en)</b> | <sup>some data may not be available</sup> |
