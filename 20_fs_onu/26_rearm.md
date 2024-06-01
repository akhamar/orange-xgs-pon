---
layout: default 
title: ONU rearm
parent: XGS-ONU-25-20NI
has_children: false
nav_order: 26
has_toc: false
---

{: .info }
> A rearm method is needed to reconfigure the ONU to keep using the modification in case of an unintentional double power failure or a double reboot of the host.
>
> After a fail safe the ONU will reconfigure itself in the default factory state. To be able to communicate with it, you will have to use the original serial number.
> 
> Bellow are examples of what can be done.

# OpnSense

## Cron Job template

Added a cron job template to rearm the module.
> `cd /usr/local/opnsense/service/conf/actions.d/`
>
> `nano actions_onu_rearm.conf`

```bash
[reload]
command:/opt/onu/fs_xgspon_mod.py
parameters:rearm %s
type:script_output
message:Rearm ONU (%s)
description:Rearm ONU
```

> `service configd restart`

To test
> `configctl -d onu_rearm reload GPONXXXXXXXX`
>
> `tail -500f /var/log/configd/configd_YYYYMMDD.log`

## Cron job usage
Added a new cron job in opnsense.
![image](https://github.com/akhamar/orange-xgs-pon/assets/32886437/61dd5c21-74fe-4b95-94a7-cad5f631aba8)

The value to put is that of the original serial GPONXXXXXXXX (and not SMBSXXXXXXXX as in the capture)
![image](https://github.com/akhamar/orange-xgs-pon/assets/32886437/2061ddff-481e-470e-872e-eef234fa24eb)


# Debian

```bash
crontab -e
```

```bash
# each 2 mins rearm ONU (only if ONU is in failsafe mode, otherwise can't access)
*/2 * * * * (echo "" && /bin/date && /opt/onu_fs/fs_xgspon_mod_release-v1.3/fs_xgspon_mod.py rearm GPONXXXXXXXX) >> /opt/onu_fs/rearm.log 2>&1

# every monday at 22:00
0 22 * * mon mv /opt/onu_fs/rearm.log /opt/onu_fs/rearm.log.1
```
