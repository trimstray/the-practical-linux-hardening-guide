## Post install tasks

### Bootloader configuration (grub)

#### :information_source: Introduction

Protection for the boot loader can prevent unauthorized users who have physical access to systems, e.g. attaining root privileges through single user mode.

Basically when you want to prohibit unauthorized reconfiguring of your system, otherwise anybody could load anything on it.

#### :eight_pointed_black_star: Protect bootloader with password

You can set password for the bootloader for prevents users from entering single user mode, changing settings at boot time, access to the bootloader console, reset the root password, if there is no password for GRUB-menu or access to non-secure operating systems.

##### Generate password hash

```bash
# Debian like distributions
grub-mkpasswd-pbkdf2

# RedHat like distributions
grub2-mkpasswd-pbkdf2
```

##### Updated grub configuration

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

###### Useful resources

- [How To Password Protect GRUB Bootloader In Linux](https://www.ostechnix.com/password-protect-grub-bootloader-linux/)

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

#### :ballot_box_with_check: Summary checklist

| <b>Item</b> | <b>True</b> | <b>False</b> |
| :---        | :---:       | :---:        |
| Set password for the bootloader | :black_square_button: | :black_square_button: |
