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

<p align="center">All suggestions and pull requests are welcome!</p>

<br>

:collision: Work in progress, just a moment... First, I update a [Table Of Content](#table-of-content).

****

## Table Of Content

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
    + [Lock the boot directory](#eight_pointed_black_star-lock-the-boot-directory)
    + [Secure /tmp and /var/tmp](#eight_pointed_black_star-secure-tmp-and-var-tmp)
    + [Disk quotas](#eight_pointed_black_star-disk-quotas)
    + [Summary checklist](#ballot_box_with_check-summary-checklist-3)
  * **[Keep system updated](#keep-system-updated)**
  * [Package management](#package-management)
    + [Automiatic security updates](#automatic-security-updates)
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
- **[Services](#hardening-services)**
  * [Disable all unnecessary](#disable-all-unnecessary)
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
    + [Apache](#apache)
    + [Securing and tuning HTTP/HTTPS protocols](#securing-and-tuning-http-https-protocols)
      - [Use HTTPS](#use-https)
      - [Enable HTTP2](#enable-http2)
      - [Separate domains](#separate-domains)
      - [Redirect all unencrypted traffic to HTTPS](#redirect-all-unencrypted-traffic-to-https)
      - [Enable HTTP Strict Transport Security](#enable-http-strict-transport-security)
      - [Security related headers](#security-related-headers)
  * [Databases](#databases)
    + [PostgreSQL](#postgresql)
    + [MySQL](#mysql)
    + [Redis](#redis)
  * [Queues](#queues)
    + [AMQP](#amqp)
- **[Deployment](#deployment)**
- **[Testing configuration](#testing-configuration)**
- **[External resources](#external-resources)**

## Pre install tasks

### Physical system security

#### :information_source: Introduction

The primary goal of many possible attacks is to stop them where possible, and failing that slow them down so that hopefully someone will notice the attacker tearing apart a system in someone's office.

#### :eight_pointed_black_star: Secure rooms

For secure rooms make sure that the walls go beyond the false ceiling, and below the raised floor, large vents should also be covered with bars if possible.

#### :eight_pointed_black_star: Monitoring

Monitoring the room with CCTV or wired cameras. It's great way to provide security for your server room or data center. As well as providing video footage of events which may occur - door open events, motion detection or any other sensor event, they also act as a visual deterrent to would be criminals.

Solution for remotely monitoring the temperature ensue proactively notify you when the temperature goes above or below pre-defined thresholds, potentially allowing you to take corrective measures before encountering costly downtime.

#### :eight_pointed_black_star: Air conditioning

Computer equipment generates heat, and is sensitive to heat, humidity, and dust, but also the need for very high resilience and failover requirements. Maintaining a stable temperature and humidity within tight tolerances is critical to IT system reliability.

Air conditioning designs for most computer or server rooms will vary depending on various design considerations, but they are generally one of two types: "up-flow" and "down-flow" configurations.

#### :eight_pointed_black_star: Fire protection

The fire protection system's main goal should be to detect and alert of fire in the early stages, then bring fire under control without disrupting the flow of business and without threatening the personnel in the facility. Server room fire suppression technology has been around for as long as there have been server rooms.

There are a series of things you need in a fire suppression system:

- an emergency power off function
- gas-based suppression system
- water detection sensors in/on the floor

#### :eight_pointed_black_star: Locked racks

All systems should be securely fastened to something with a cable system, or locked in an equipment cage if possible. Case locks should be used when possible to slow attackers down.

#### :eight_pointed_black_star: Console security

With physical access to most machines you can simply reboot the system and ask it nicely to launch into single user mode, or tell it to use `/bin/sh` for init.

#### :eight_pointed_black_star: BIOS protection

In the program itself to edit the BIOS settings:

- only boot from specific drive
- disable the unused controllers
- disable the booting from external media devices (USB/CD/DVD)
- enable BIOS password

You need to protect the BIOS of the host with a password so the end-user won’t be able to change and override the security settings in the BIOS.

Main reasons for password protecting the BIOS:

- preventing changes to BIOS settings
- preventing system booting

Because the methods for setting a BIOS password vary between computer manufacturers, consult the computer's manual for specific instructions.

  > For this reason, it is good practice to lock the computer case if possible. However, consult the manual for the computer or motherboard before attempting to disconnect the CMOS battery.

#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
| Physically secure machine (also outside of a server room) | :black_square_button: | :black_square_button: |
| Monitoring server rooms with CCTV or wired cameras | :black_square_button: | :black_square_button: |
| Remotely monitoring the temperature | :black_square_button: | :black_square_button: |
| Efficient air conditioning solution | :black_square_button: | :black_square_button: |
| Efficient fire protection system | :black_square_button: | :black_square_button: |
| Locked cage (server case) | :black_square_button: | :black_square_button: |
| Physical access to server console | :black_square_button: | :black_square_button: |
| Password on the BIOS | :black_square_button: | :black_square_button: |
| Disable external media devices | :black_square_button: | :black_square_button: |
| Periodic physical inspections | :black_square_button: | :black_square_button: |

### Hard disk encryption

#### :information_source: Introduction

Disk encryption is focused on securing physical access, while relying on other parts of the system to provide things like network security and user-based access control.

Most of the Linux distributions will allow you to encrypt your disks before installation.

If you use an alternative installation method (e.g. from `debootstrap`) you can create an [encrypted disk manually](#disk-partitions).

Before this you should to answer the following questions:

- What part of filesystem do you want to encrypt?
  * only user data
  * user data and system data
- How should `swap`, `/tmp` and other be taken care of?
  * disable or mount as ramdisk
  * encrypt (separately of as part of full)
- How should encrypted parts of the disk be unlocked?
  * passphrase
  * key file
- When should encrypted parts of the disk be unlocked?
  * before boot process
  * during boot process
  * mixed above or manually

#### :eight_pointed_black_star: Encrypt root filesystem

Unlocked during boot, using passphrases or USB stick with keyfiles.

#### :eight_pointed_black_star: Encrypt /boot partition

- encrypting the whole disk without `/boot` partition but keeping it on a flash drive you carry at all times
- using a checksum value of the boot sector
- boot partition to detect it and change you passphrase

This may not completely get rid of the attack vector described in this post as there is still part of the bootloader that isn't encrypted, but at least the grub stage2 and the kernel/ramdisk are encrypted and should make it much harder to attack.

In addition, the `/boot` partition may be a weak point if you use encryption methods for the rest of the disk.

Historically it has been necessary to leave `/boot` unencrypted because bootloaders didn't support decrypting block devices. However, there are some dangers to leaving the bootloader and ramdisks unencrypted.

Before this you should to answer the following questions:

- Where your `/boot` partition is stored?
  * the same place where stored `/`
  * separately partition
  * external flash drive

The following recipe should be made after installing the system (however, these steps are included in this section to avoid mixing issues).

###### Create copy of your /boot

```bash
mkdir /mnt/boot
mount --bind / /mnt/boot
rsync -aAXv /boot/ /mnt/boot/
umount /mnt/boot
```

###### Removed old /boot partition

```bash
umount /boot
sed -i -e '/\/boot/d' /etc/fstab
```

###### Regenerate grub configuration

```bash
# Debian like distributions
grub-mkconfig > /boot/grub/grub.cfg

# RedHat like distributions
grub2-mkconfig > /boot/grub2/grub.cfg
```

###### Enable `GRUB_ENABLE_CRYPTODISK` param

```bash
echo GRUB_ENABLE_CRYPTODISK=y >> /etc/default/grub
```

###### Reinstall grub

```bash
# Debian like distributions
grub-install /dev/sda

# RedHat like distributions
grub2-install /dev/sda
```

  > More details can be found here (Bootloader configuration (grub) section):
  > - [Lock the boot directory](#eight_pointed_black_star-lock-the-boot-directory)

#### :eight_pointed_black_star: Swap partition

- swap area is not required to survive a reboot, therefore a new random encryption key can be chosen each time the swap area is activated
- get the key from `/dev/urandom` because `/dev/random` maybe stalling your boot sequence

  > More details can be found here (Bootloader configuration (grub) section):
  > - [Swap partition](#eight_pointed_black_star-swap-partition-1)

#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
| Encrypting the whole disk | :black_square_button: | :black_square_button: |
| Usage passphrase or key file to disk unlocked | :black_square_button: | :black_square_button: |
| Choosing a strong passphrase | :black_square_button: | :black_square_button: |
| Encrypting the `/boot` partition | :black_square_button: | :black_square_button: |
| Securing swap partition with `/dev/urandom` | :black_square_button: | :black_square_button: |
| `swap` or `tmp` using an automatically generated per-session throwaway key | :black_square_button: | :black_square_button: |

## Post install tasks

### Bootloader configuration (grub)

#### :information_source: Introduction

Protection for the boot loader can prevent unauthorized users who have physical access to systems, e.g. attaining root privileges through single user mode.

Basically when you want to prohibit unauthorized reconfiguring of your system, otherwise anybody could load anything on it.

#### :eight_pointed_black_star: Protect bootloader with password

You can set password for the bootloader for prevents users from entering single user mode, changing settings at boot time, access to the bootloader console, reset the root password, if there is no password for GRUB-menu or access to non-secure operating systems.

#### :eight_pointed_black_star: Protect bootloader config files

Set the owner and group of `/etc/grub.conf` to the root user:

```bash
chown root:root /etc/grub.conf
```

or

```bash
chown -R root:root /etc/grub.d
```

Set permission on the `/etc/grub.conf` or `/etc/grub.d` file to read and write for root only:

```bash
chmod og-rwx /etc/grub.conf
```

or

```bash
chmod -R og-rwx /etc/grub.d
```

###### Generate password hash

```bash
# Debian like distributions
grub-mkpasswd-pbkdf2

# RedHat like distributions
grub2-mkpasswd-pbkdf2
```

###### Updated grub configuration

```bash
cat > /etc/grub.d/01_hash << __EOF__
set superusers="user"
password_pbkdf2 user
grub.pbkdf2.sha512.<hash> # rest of your password hash
__EOF__
```

And regenerate grub configuration:

```bash
# Debian like distributions
grub-mkconfig > /boot/grub/grub.cfg

# RedHat like distributions
grub2-mkconfig > /boot/grub2/grub.cfg
```

#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
| Set password for the bootloader | :black_square_button: | :black_square_button: |

### Disk partitions

#### :information_source: Introduction

Critical file systems should be separated into different partitions in ways that make your system a better and more secure.

#### :eight_pointed_black_star: Separate disk partitions

Make sure the following filesystems are mounted on separate partitions:

- `/boot`
- `/tmp`
- `/var`
- `/var/tmp` (or symlink for `/tmp`)
- `/var/log`

Additionally, depending on the purpose of the server, you should consider separating the following partitions:

- `/usr`
- `/home`
- `/var/www`

#### :eight_pointed_black_star: Read-only boot directory

The boot directory contains important files related to the Linux kernel, so you need to make sure that this directory is locked down to read-only permissions.

Add **ro** option to `/etc/fstab` for **/boot** entry:

```bash
LABEL=/boot   /boot   ext2  defaults,ro   1 2
```

#### :eight_pointed_black_star: Secure /tmp, /var/tmp and /dev/shm



#### :eight_pointed_black_star: Swap partition

In addition, the `/boot` partition may be a weak point if you use encryption methods for the rest of the disk.

#### :eight_pointed_black_star: Disk quotas

In addition, the `/boot` partition may be a weak point if you use encryption methods for the rest of the disk.

#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
| Separate `/boot` partition | :black_square_button: | :black_square_button: |
| `/boot` partition located on external drive | :black_square_button: | :black_square_button: |
