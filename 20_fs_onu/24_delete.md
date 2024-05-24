---
layout: default 
title: ONU modifications removal
parent: XGS-ONU-25-20NI
has_children: false
nav_order: 24
has_toc: false
---

## Removing the mod

Enter shell mode then remove the mod
```bash
./fs_xgspon_mod.py telnet SMBSXXXXXXXX

/system/sh

cd /mnt/rwdir

rm setup.sh

reboot
```