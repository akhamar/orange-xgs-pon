---
layout: default 
title: ONT Configuration
parent: LXE-010X-A
has_children: false
nav_order: 42
has_toc: false
---

# Table of Contents
{: .no_toc }

- TOC
{:toc}

# Backing up

Before flashing new parameters, save the current (factory) configuration as a backup. This precaution ensures you can restore the original settings if needed.

## Accessing shell

Use Telnet and the [previously provided credentials](41_update.html#ont-credentials) to access the ONT. 

```
telnet 192.168.100.1
Trying 192.168.100.1...
Connected to 192.168.100.1.
Escape character is '^]'.
LXE-010X-A login: leox
Password: leolabs_7
#
```

## Retrieving current configuration settings

```
flash get GPON_SN
flash get PON_VENDOR_ID
flash get HW_HWVER
```

Copy the output values somewhere.

# Updating configuration settings

To update the settings with your Livebox details:

```
flash set GPON_SN <YOUR_LIVEBOX_ONT_SERIAL>
flash set PON_VENDOR_ID SMBS
flash set HW_HWVER SMBSXLB7400
```

Reboot the ONT using the shell command `reboot`. Then, connect it to your router’s WAN port and configure the following:
- VLAN: 832
- MAC address cloning (from your Livebox)
- DHCP CoS 6 + options 60/77/90

You can use [GO-BOX](https://github.com/Stoufiler/GO-BOX) to simplify the process by copying and pasting the required values.
