---
layout: home
title: Home
has_children: false
nav_order: 10
has_toc: false
---

# Overview
This guide explains how to configure an **XGS-PON ONU/ONT module** to bypass Orange Livebox.

{: .important }
> These steps are only compatible with the three ONU/ONT models listed below. Other models were tested but do not work properly for Orange Livebox bypass.

| Model           | Chipset          | Manufacturer | Order link                                                                                                                                                                                             |
|-----------------|------------------|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| XGS-ONU-25-20NI | CIG XG-99S       | FS.com       | - [fs.com](https://www.fs.com/fr/products/185594.html)                                                                                                                                                 |
| WAS-110         | MaxLinear PRX126 | Azores       | - [fibermall.com](https://www.fibermall.com/sale-460693-xgspon-onu-sfp-stick.htm)<br>- [aliexpress (chose 8311 Version)](https://www.aliexpress.us/item/1005007856556526.html?gatewayAdapt=4itemAdapt) |
| LXE-010X-A      | Realtek RTL9615C | Leox         | - [leolabs.pl](https://www.leolabs.pl/ont-leox-lxe-010x-a.html)                                                                                                                                        |

## Recommendations
I strongly recommand the **WAS-110** with the custom firmware 8311 as it's the most advanced ONU of all, which allow a better support, as well as also massively tested against many different ISP and in many country with a huge base of users using it successfuly.

The custom firmware is actively worked on with addons, features, corrections and support added all the time.

## Special thanks
- [lama](https://github.com/palpaga) for assistance in understanding the issues.
- [djGrrr](https://github.com/djGrrr) for help with WAS-110 debugging, troubleshooting, and community firmware.
- [rss](https://github.com/rssor) for the beautiful mod on the XGS-ONU-25-20NI ONU from fs.com.

## Additional resources
- [8311](https://pon.wiki)
- [PON Madness](https://hackaday.io/project/194709-pon-madness-bypass-xgs-pon-ontswith-a-stick)

# Configuration guides
- FS [XGS-ONU-25-20NI](20_fs_onu.html) (CIG XG-99S)
- Azores [WAS-110](30_was_onu.html) (MaxLinear PRX126)
- Leox [LXE-010X-A](40_leox_ont.html) (Realtek RTL9615C)

<!--
 {% t global.tagline %}
-->
