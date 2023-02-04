---
layout: post
title:  "Notes on enabling full-disk encryption on existing Arch Linux system"
---

Some time ago, I decided to upgrade the hard drives (whose count is 2) on one of my old laptops which runs Arch Linux, and at the same time to enable full-disk encryption (FDE).

When installing a fresh system, it`s easy and straightforward to enable a FDE, and the Arch manual completely covers it. 
However, as I wanted to transfer all the data and preserve the exact state of the system, there were some things to care about. The key point here is that one can not just encrypt the system by simple means like setting a checkbox, because it requires hard drives to be formatted. So from this perspective the migration looks like you have changed drives.
Worth to mention, I am using a [LUKS on LVM scheme](https://wiki.archlinux.org/title/dm-crypt/Encrypting_an_entire_system#LUKS_on_LVM) in my devices.

Here are my tips from the latest migration

* TAR is still a great tool for [system backups](https://wiki.archlinux.org/title/Full_system_backup_with_tar). You don`t need to install additional utils for restoring.
* If there are multiple hard drives in the system, you probably want to decrypt all with typing a password only once. Nice trick for achieving it is to use a [crypttab](https://wiki.archlinux.org/title/dm-crypt/Encrypting_an_entire_system#Configuring_fstab_and_crypttab) and a keyfile for decrypting a non-system drive, which is stored on the system dir, e.g. /etc/decrypt_key.
So, /etc/crypttab should look like this
```bash
# <name>        <device>        <password>              <options>
second_hdd      /dev/sda1       /etc/decrypt_key
```

* It makes sense to back up/home or another non-system directory to a separate file. Just be ready that your restored system will not work from the first attempt (let`s say, smth is forgotten or misconfigured), but you have already spent a lot of time restoring your photos and other volume-consuming stuff.

* Before migration, make the system up-to-date. You\`ll probably need to install additional libs so it`s better to not deal with missing and/or conflicting packages during the process.

* There are probably a lot of non-critical cache files from utils like `yay`, `npm`, `docker` often measured in gigabytes, and it is nice to remove them before backing the system up. You don`t want to spend additional hours moving the cache between hard drives.

* A good way to practice formatting your hard drives is to play the whole scenario on VMs. One thing worth mentioning here - don't forget to enable EFI boot mode (of course, if your machine also has it). Example for Virtual Box [here](https://www.makeuseof.com/set-up-efi-linux-virtual-machine-virtualbox/). This feature is usually disabled by default and Arch installation will look different then.

* Finally, after everything is migrated, fully encrtypted and working as expected, do not forget to <i>securely</i> remove your backups from unencrypted drives. 

Happy encrypting!