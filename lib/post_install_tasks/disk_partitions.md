## Post install tasks

### Disk partitions

#### :information_source: Introduction

Critical file systems should be separated into different partitions in ways that make your system a better and more secure.

#### :eight_pointed_black_star: Separate disk partitions

Make sure the following filesystems are mounted on separate partitions:

- `/boot`
- `/tmp`
- `/var`
- `/var/log`

Additionally, depending on the purpose of the server, you should consider separating the following partitions:

- `/usr`
- `/home`
- `/var/www`

You should also consider separating these partitions:

- `/var/tmp`
- `/var/log/audit`

###### Useful resources

- [Recommended partitioning scheme](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/installation_guide/s2-diskpartrecommend-x86)
- [Most secure way to partition linux?](https://security.stackexchange.com/questions/38793/most-secure-way-to-partition-linux)

#### :eight_pointed_black_star: Mount options: nodev, nosuid and noexec

For more security-focused situations is as follows:

- `nodev` - specifies that the filesystem cannot contain special devices: This is a security precaution. You don't want a user world-accessible filesystem like this to have the potential for the creation of character devices or access to random device hardware
- `nosuid` - specifies that the filesystem cannot contain set userid files. Preventing setuid binaries on a world-writable filesystem makes sense because there's a risk of root escalation or other awfulness there
- `noexec` - this param might be useful for a partition that contains no binaries, like **/var**, or contains binaries you do not want to execute on your system (from partitions with `noexec`), or that cannot even be executed on your system

###### Useful resources

- [Linux Security: Mount /tmp With nodev, nosuid, and noexec Options](https://www.cyberciti.biz/faq/linux-add-nodev-nosuid-noexec-options-to-temporary-storage-partitions/)
- [Security Handbook/Mounting partitions](https://wiki.gentoo.org/wiki/Security_Handbook/Mounting_partitions)

#### :eight_pointed_black_star: Secure /boot directory

The boot directory contains important files related to the Linux kernel, so you need to make sure that this directory is locked down to read-only permissions.

Add **ro** option and `nodev`, `nosuid` and `noexec` to `/etc/fstab` for **/boot** entry:

```bash
LABEL=/boot  /boot  ext2  defaults,ro,nodev,nosuid,noexec  1 2
```

  > When updating the kernel you will have to move the flag to `rw`:
  > ```bash
  > mount -o remount,defaults,rw /boot
  > ```

#### :eight_pointed_black_star: Secure /tmp and /var/tmp

On Linux systems, the **/tmp** and **/var/tmp** locations are world-writable.

Several daemons/applications use the **/tmp** or **/var/tmp** directories to temporarily store data, log information, or to share information between their sub-components. However, due to the shared nature of these directories, several attacks are possible, including:

- Leaks of confidential data via secrets in file names
- Race-condition attacks (TOCTOU) on the integrity of processes and data
- Denial-of-Service (DoS) attacks based on race conditions and pre-allocating file/directory names

As a rule of thumb, malicious applications usually write to **/tmp** and then attempt to run whatever was written. A way to prevent this is to mount **/tmp** on a separate partition with the options `nodev`, `nosuid` and `noexec` enabled.

This will deny binary execution from **/tmp**, disable any binary to be suid root, and disable any block devices from being created.

**The first possible scenario is create symlink**

```bash
mv /var/tmp /var/tmp.old
ln -s /tmp /var/tmp
cp -prf /var/tmp.old/* /tmp && rm -fr /var/tmp.old
```

and set properly mount params:

```bash
UUID=<...>  /tmp  ext4  defaults,nodev,nosuid,noexec  1 2
```

**The second scenario is a bind mount**

The storage location **/var/tmp** should be bind mounted to **/tmp**, as having multiple locations for temporary storage is not required:

```bash
/tmp  /var/tmp  none  rw,nodev,nosuid,noexec,bind  0 0
```

**The third scenario is setting up polyinstantiated directories**

Create new directories:

```bash
mkdir --mode 000 /tmp-inst
mkdir --mode 000 /var/tmp/tmp-inst
```

Edit `/etc/security/namespace.conf`:

```bash
 /tmp      /tmp-inst/          level  root,adm
 /var/tmp  /var/tmp/tmp-inst/  level  root,adm
```

Set correct **SELinux** context:

```bash
setsebool polyinstantiation_enabled=1
chcon --reference=/tmp /tmp-inst
chcon --reference=/var/tmp/ /var/tmp/tmp-inst
```

And set `nodev`, `nosuid` and `noexec` mount options in `/etc/fstab`.

  > Alternative for **polyinstantiated directories** is **PrivateTmp** feature available from **systemd**. For more information please see: [New Red Hat Enterprise Linux 7 Security Feature: PrivateTmp](https://access.redhat.com/blogs/766093/posts/1976243).

###### Useful resources

- [Increasing Linux server security with nodev, nosuid and no exec options](https://kb.iweb.com/hc/en-us/articles/230267488--Increasing-Linux-server-security-with-nodev-nosuid-and-no-exec-options)
- [Why it is important to Securing /dev/shm and /tmp](https://askubuntu.com/questions/389408/why-it-is-important-to-securing-dev-shm-and-tmp)

#### :eight_pointed_black_star: Secure /dev/shm

`/dev/shm` is a temporary file storage filesystem, i.e. **tmpfs**, that uses RAM for the backing store. One of the major security issue with the `/dev/shm` is anyone can upload and execute files inside the `/dev/shm` similar to the `/tmp` partition. Further the size should be limited to avoid an attacker filling up this mountpoint to the point where applications could be affected. (normally it allows 20% or more of RAM to be used). The sticky bit should be set like for any world writeable directory.

For applies to shared memory `/dev/shm` mount params:

```bash
tmpfs  /dev/shm  tmpfs  rw,nodev,nosuid,noexec,size=1024M,mode=1777 0 0
```

  > You can also create a group named 'shm' and put application users for SHM-using applications in there. Then the access can be completely be restricted as such:

```bash
tmpfs  /dev/shm  tmpfs  rw,nodev,nosuid,noexec,size=1024M,mode=1770,uid=root,gid=shm 0 0
```

###### Useful resources

- [Securing /dev/shm partition](https://www.gnutoolbox.com/securing-devshm-partition/)

#### :eight_pointed_black_star: Secure /proc filesystem

The proc pseudo-filesystem `/proc` should be mounted with `hidepid`. When setting `hidepid` to **2**, directories entries in `/proc` will hidden.

```bash
proc  /proc  proc  defaults,hidepid=2  0 0
```

  > Some of the services/programs operate incorrectly when the `hidepid` parameter is set, e.g. Nagios checks.

###### Useful resources

- [Linux system hardening: adding hidepid to /proc mount point](https://linux-audit.com/linux-system-hardening-adding-hidepid-to-proc/)

#### :eight_pointed_black_star: Swap partition

Encryption of swap space is used to protect sensitive information. It improves the availability of the system, which is also an important part of information security.

```bash
# Turn off the swap area
swapoff -a

# Wipe the swap area
shred -vfz -n 10 /dev/sda2

# Update /etc/fstab
UUID=7e1e715e-7ac4-45ad-b029-18fed80f225f none swap defaults 0 0

# Add the swap area to /etc/crypttab
swap /dev/sda2 /dev/urandom swap

# Activate the mapping
cryptdisks_start swap
/etc/init.d/cryptdisks restart

# Add the encrypted swap area to /etc/fstab
/dev/mapper/swap none swap defaults 0 0

# Turn on the swap area
swapon -a
```

###### Useful resources

- [dm-crypt/Swap encryption](https://wiki.archlinux.org/index.php/Dm-crypt/Swap_encryption)
- [Encrypted swap partition on Debian/Ubuntu](https://feeding.cloud.geek.nz/posts/encrypted-swap-partition-on/)

#### :eight_pointed_black_star: Disk quotas

#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
| Separate base partition scheme: `/boot`, `/tmp`, `/var`, `/var/log` | :black_square_button: | :black_square_button: |
| Separate `/usr` partition | :black_square_button: | :black_square_button: |
| Separate `/home` partition | :black_square_button: | :black_square_button: |
| Separate `/var/www` partition | :black_square_button: | :black_square_button: |
| Separate `/var/tmp` partition | :black_square_button: | :black_square_button: |
| Separate `/var/audit` partition | :black_square_button: | :black_square_button: |
| Secure `/boot` directory with `ro`, `nodev`, `nosuid`, `noexec` options | :black_square_button: | :black_square_button: |
| Secure `/tmp` and `/var/tmp` directory with `nodev`, `nosuid`, `noexec` options | :black_square_button: | :black_square_button: |
| Create symlink for `/var/tmp` in `/tmp` | :black_square_button: | :black_square_button: |
| Setting up bind-mount `/var/tmp` to `/tmp` | :black_square_button: | :black_square_button: |
| Setting up polyinstantiated directories for `/tmp` and `/var/tmp` | :black_square_button: | :black_square_button: |
| Secure `/dev/shm` directory with `nodev`, `nosuid`, `noexec` options | :black_square_button: | :black_square_button: |
| Secure `/proc` filesystem with `hidepid=2` option | :black_square_button: | :black_square_button: |
| Secure swap area with cryptsetup | :black_square_button: | :black_square_button: |