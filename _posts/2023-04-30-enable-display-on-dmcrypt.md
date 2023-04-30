---
layout: post
title:  "Enable external display for dmcrypt promtp"
---
Occasionally I use my laptop in docked mode. As always, I have a full-disk encryption [made with dmcrypt](/2023/02/04/notes-on-fde-arch-linux.html) but the prompt for typing the password is visible on the built display only. It is an expected behavior because the graphic module is not initialized yet. 

This makes things a bit inconvenient when you need to restart the system - because you'll need to open the lid, type a password and close it back.

Hopefully, there's a standard solution for the problem: loading a graphic module with [mkinitcpio](https://wiki.archlinux.org/title/Mkinitcpio#MODULES)
1. Add the module to MODULES section. If you have Intel graphics, i915 should work in most cases
```
# /etc/mkinitcpio.conf
MODULES=(i915?)
```

2. Regenerate initramfs from preset
```bash
mkinitcpio -p linux
```
As Arch docs suggest, adding `?` to the end of the module name will make it optional, so no error is thrown if missing.

Once the initramfs is regenerated with the i915 module included, the external display should work during the dmcrypt-prompt stage.

Kudos to the Arch community 👍
