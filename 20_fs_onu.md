---
layout: default 
title: XGS-ONU-25-20NI
has_children: true
nav_order: 20
has_toc: false
---

# Introduction

The ONU FS (XGS-ONU-25-20NI) has a limit of 17 mappable VLANs on the bridge. This can therefore pose a problem in the case where the OLT goes back a quantity greater than 17 VLANs mapping.

This UN can be found here: https://www.fs.com/fr/products/185594.html

A set of sources on the ONU can be found here: https://hack-gpon.org/xgs/ont-fs-XGS-ONU-25-20NI/

This is not a tutorial on how to make a DHCP request with prio 6 on VLAN832. The information is here only to configure an ONU so that it can receive traffic from the OLT and transmit.

Are you bricking your ONU ? I don't care, not my problem :p


# Explanation of the problem

The ONU is limited to 17 VLAN rules mapping. Neither of the two people who managed to make the ONU work had the TV option.
The TV option takes 6x 840VLAN rules + 3x 838VLAN rules.
This explains the difference in the quantity of VLAN rules. 13 VLAN rules for them, 22 for me (13 + 6 + 3 = 22).

However, VLANs 838 and 840 are sent by the OLT before VLAN 832. VLAN 832 is therefore not mapped on the bridge because it is the 19th rule sent (beyond 17). It therefore becomes impossible to pass frames on vlan832.

{: .info }
> 95% of people with an Orange offer are therefore affected by this problem. The ONU mod having been finished, this will allow you to have a functional line with this ONU


## Case number 1 => you do not have the TV option

Being limited to around 13 VLANs, you should not have any problem and therefore a simple configuration of the module will be sufficient.


## Case number 2 => you have the TV option

Being most likely with more than 22 VLANs, you should have the problem and therefore a simple configuration of the module will not be sufficient.
You will therefore need to do a little more than simple configuration.


# Good practice

Directly changing the serial, vendor and hardware version values ​​on the ONU is not recommended. Indeed, in the case of RMA, you will need to go back to the original state of the ONU.
Likewise, the ONU has a set of config files that allow these values ​​to be dynamically replaced, without having to change the default values. This method is therefore greatly favored and recommended.

An ONU must have a failsafe which allows you to return to the initial state in the event of a brick or bad configuration. The mod that is used to configure the ONU allows you to perform a factory reset of the ONU via a double power cycle of less than 30 to 120 seconds.
This makes it possible to greatly limit unintentional bricks caused by poor handling. This also makes it easy to return the ONU to factory settings (just do a double power cycle of less than 120sec).


# Material/Software validation

Router:
- OpnSense
- Debian

NIC:
- X710-DA2 (ONU is only accessible when fiber is plugged in)
- X520-DA1
- X520-DA2
- N20KJ [Broadcom 57810 S]
- Mellanox MT27710 [ConnectX-4 Lx]

Media converter:
- MC220L v2.x (ONU is accessible with/without fiber plugged in)
- MC220L v3.x (ONU is accessible with plugged fiber)