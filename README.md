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

## Table Of Contents

- **[Contributing](#contributing)**
- **[Pre install tasks](#pre-install-tasks)**
  * **[Physical system security](#physical-system-security)**
    + [Introduction](#information_source-introduction)
    + [Secure rooms](#eight_pointed_black_star-secure-rooms)
    + [Monitoring](#eight_pointed_black_star-monitoring)
    + [Air conditioning](#eight_pointed_black_star-air-conditioning)
    + [Fire protection](#eight_pointed_black_star-fire-protection)
    + [Locked racks](#eight_pointed_black_star-locked-racks)
    + [Console security](#eight_pointed_black_star-console-security)
    + [BIOS protection](#eight_pointed_black_star-bios-protection)
    + [Summary checklist](#ballot_box_with_check-summary-checklist)
  * **[Hard disk encryption](#hard-disk-encryption)**
    + [Introduction](#information_source-introduction-1)
    + [Encrypt root filesystem](#eight_pointed_black_star-encrypt-root-filesystem)
    + [Encrypt /boot partition](#eight_pointed_black_star-encrypt-boot-partition)
    + [Swap partition](#eight_pointed_black_star-swap-partition)
    + [Summary checklist](#ballot_box_with_check-summary-checklist-1)
- **[Post install tasks](#post-install-tasks)**
  * **[Bootloader configuration (grub)](#bootloader-configuration-grub)**
    + [Introduction](#information_source-introduction-2)
    + [Protect bootloader with password](#information_source-protect-bootloader-with-password)
    + [Protect bootloader config files](#information_source-protect-bootloader-config-files)
    + [Summary checklist](#ballot_box_with_check-summary-checklist-2)
  * **[Disk partitions](#disk-partitions)**
    + [Introduction](#information_source-introduction-3)
    + [Separate disk partitions](#eight_pointed_black_star-separate-disk-partitions)
    + [Mount options: nodev, noexec and nosuid](#eight_pointed_black_star-mount-options-nodev-noexec-and-nosuid)
    + [Secure /boot directory](#eight_pointed_black_star-secure-boot-directory)
    + [Secure /tmp and /var/tmp](#eight_pointed_black_star-secure-tmp-and-vartmp)
    + [Secure /dev/shm](#eight_pointed_black_star-secure-devshm)
    + [Secure /proc filesystem](#eight_pointed_black_star-secure-proc-filesystem)
    + [Swap partition](#eight_pointed_black_star-swap-partition-1)
    + [Disk quotas](#eight_pointed_black_star-disk-quotas)
    + [Summary checklist](#ballot_box_with_check-summary-checklist-3)
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
  * [Disable all unnecessary services](#disable-all-unnecessary-services)
    + [Common unix print system](#eight_pointed_black_star-common-unix-print-system)
    +  [Summary Checklits](#ballot_box_with_check-summary-checklist-4)
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
  * [Web services](#web-services)
    + [Nginx](#nginx)
      - [Files and directories permissions](#files-and-directories-permissions)
      - [Use HTTPS](#use-https)
      - [Enable HTTP2](#enable-http2)
      - [Diffie Hellman Ephemeral Parameter](#diffie-hellman-ephemeral-parameter)
      - [Separate domains](#separate-domains)
      - [Redirect all unencrypted traffic to HTTPS](#redirect-all-unencrypted-traffic-to-https)
      - [Enable HTTP Strict Transport Security](#enable-http-strict-transport-security)
      - [Security related headers](#security-related-headers)
    + [Apache](#apache)
  * [Databases](#databases)
    + [PostgreSQL](#postgresql)
    + [MySQL](#mysql)
    + [Redis](#redis)
  * [Queues](#queues)
    + [AMQP](#amqp)
- **[Deployment](#deployment)**
- **[Testing configuration](#testing-configuration)**
- **[External resources](#external-resources)**

## Contributing

If you find something which doesn't make sense, or one of these doesn't seem right, or something seems really stupid; please make a pull request or please add valid and well-reasoned opinions about your changes or comments.

Before add pull request please see **[this](CONTRIBUTING.md)**.
