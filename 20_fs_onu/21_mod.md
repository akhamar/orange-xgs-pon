---
layout: default 
title: ONU modification
parent: XGS-ONU-25-20NI
has_children: false
nav_order: 21
has_toc: false
---

# List of essentials

Version 1.3 of the mod is available here: [rssor mod v1.3](https://github.com/rssor/fs_xgspon_mod/releases/download/v1.3/fs_xgspon_mod_release.tgz)
The explanations (English) are available here: [readme](https://github.com/rssor/fs_xgspon_mod/tree/test_bruteforce_and_orange_support)
The explanations (English) for the mod in V1.3 are available here: [readme](https://github.com/rssor/fs_xgspon_mod)

You will need to know the ONU serial. The easiest way to do this is to request it from fs.com.
In case you have forgotten, there is a sub-module in the mod which allows you to find this serial in 20 seconds ([Serial recovery](https://akhamar.github.io/orange-xgs-pon/20_fs_onu/25_serial_recovery.html))

# Installing the mod

Make sure you are on the ONU host machine. You will need an address on the `192.168.100.0/24` network. You will also need to have a firewall rule that allows the ONU to access port 8172 on the address you have chosen on the network `192.168.100.0/24`.
The ONU is accessible on the IP `192.168.100.1`

In our case, ISP orange the commands to do are as follows.


## Installation

{: .important }
> => In case you are not sure if you have less than 17 vlan rules to map

```bash
./fs_xgspon_mod.py install GPONXXXXXXXX orange SMBSXXXXXXXX
```
> Where `GPONXXXXXXXX` is the original ONU fs.com serial and `SMBSXXXXXXXX` is the livebox serial

> ONU reboot (press enter)

{: .important }
> => In case you are sure you have less than 17 vlan rules to map

```bash
./fs_xgspon_mod.py install GPONXXXXXXXX orange SMBSXXXXXXXX --vlan_rules ""
```
> Where `GPONXXXXXXXX` is the original ONU fs.com serial and `SMBSXXXXXXXX` is the livebox serial

> ONU reboot (press enter)