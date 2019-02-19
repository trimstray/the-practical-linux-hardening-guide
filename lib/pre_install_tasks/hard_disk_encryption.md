## Pre install tasks

### Hard disk encryption

#### :information_source: Introduction

Disk encryption is focused on securing physical access, while relying on other parts of the system to provide things like network security and user-based access control.

Most of the Linux distributions will allow you to encrypt your disks before installation.

If you use an alternative installation method (e.g. from `debootstrap`) you can create an [encrypted disk manually](lib/post_install_tasks/disk_partitions.md#disk-partitions).

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

###### Useful resources

- [dm-crypt/Encrypting an entire system](https://wiki.archlinux.org/index.php/Dm-crypt/Encrypting_an_entire_system)

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

##### Create copy of your /boot

```bash
mkdir /mnt/boot
mount --bind / /mnt/boot
rsync -aAXv /boot/ /mnt/boot/
umount /mnt/boot
```

##### Removed old /boot partition

```bash
umount /boot
sed -i -e '/\/boot/d' /etc/fstab
```

##### Regenerate grub configuration

```bash
# Debian like distributions
grub-mkconfig > /boot/grub/grub.cfg

# RedHat like distributions
grub2-mkconfig > /boot/grub2/grub.cfg
```

##### Enable `GRUB_ENABLE_CRYPTODISK` param

```bash
echo GRUB_ENABLE_CRYPTODISK=y >> /etc/default/grub
```

##### Reinstall grub

```bash
# Debian like distributions
grub-install /dev/sda

# RedHat like distributions
grub2-install /dev/sda
```

  > More details can be found here [Bootloader configuration (grub) section](lib/post_install_tasks/bootloader_configuration.md#bootloader-configuration-grub)

###### Useful resources

- [Encrypting More: /boot Joins The Party](https://dustymabe.com/2015/07/06/encrypting-more-boot-joins-the-party/)
- [Encrypting the /boot partition in a Linux system can protect from an Evil Maid Attack?](https://security.stackexchange.com/questions/166075/encrypting-the-boot-partition-in-a-linux-system-can-protect-from-an-evil-maid-a)

#### :eight_pointed_black_star: Swap partition

- swap area is not required to survive a reboot, therefore a new random encryption key can be chosen each time the swap area is activated
- get the key from `/dev/urandom` because `/dev/random` maybe stalling your boot sequence

  > More details can be found here [Swap partition](lib/post_install_tasks/disk_partitions.md#eight_pointed_black_star-swap-partition)

###### Useful resources

- [An introduction to swap space on Linux systems](https://opensource.com/article/18/9/swap-space-linux-systems)

#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
| Encrypting the whole disk | :black_square_button: | :black_square_button: |
| Usage passphrase or key file to disk unlocked | :black_square_button: | :black_square_button: |
| Choosing a strong passphrase | :black_square_button: | :black_square_button: |
| Encrypting the `/boot` partition | :black_square_button: | :black_square_button: |
| Securing swap partition with `/dev/urandom` | :black_square_button: | :black_square_button: |
| `swap` or `tmp` using an automatically generated per-session throwaway key | :black_square_button: | :black_square_button: |
