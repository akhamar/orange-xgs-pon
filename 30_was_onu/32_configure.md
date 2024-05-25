---
layout: default 
title: ONU Configuration
parent: WAS-110
has_children: false
nav_order: 32
has_toc: false
---


# Configuring the ONU

Navigate to the ONU community interface. And login.

> [https://192.168.11.1](https://192.168.11.1)

On the menu and under 8311 go to configuration.

![image](https://raw.githubusercontent.com/akhamar/orange-xgs-pon/main/assets/images/was-110/WAS-110-community-configuration.png)


## PON

Set your LiveBox values and save.

You will need to set the `PON Serial Number`, the `Vendor ID` and the `Hardware Version`.

| PON Serial Number | YOUR_LIVEBOX_ONT_SERIAL |
| Vendor ID         | SMBS                    |
| Hardware Version  | SMBSXLB7400             |

![image](https://raw.githubusercontent.com/akhamar/orange-xgs-pon/main/assets/images/was-110/WAS-110-community-configuration-values-01.png)


## ISP Fixes

Unset the `Fix VLANs` and save.

![image](https://raw.githubusercontent.com/akhamar/orange-xgs-pon/main/assets/images/was-110/WAS-110-community-configuration-values-02.png)


