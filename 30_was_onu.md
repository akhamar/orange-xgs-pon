---
layout: default 
title: WAS-110
has_children: true
nav_order: 30
has_toc: false
---

# Table of Contents
{: .no_toc }

- TOC
{:toc}

# Introduction

The WAS-110 firmware can be switched to a community firmware that allow a lot of customization and controle over the ONU.

# Material/Software validation

Router (soft):
- OpnSense
- Debian
- OpenWrt

Router (hardware):
- tp-link er8411
- mikrotik CCR2004
- Banana Pi BPI-R4

~~NIC:~~
- ~~X710-DA2 (some seem to have issues, I didn't)~~
- ~~X520-xx~~
- ~~Mellanox MT27710 [ConnectX-4 Lx]~~

{: .warning }
> Do not use any NIC to host the ONU as above 7800-8000Mbps the ONU will draw too much power and enter a deep emergency lock state.
> 
> Use a switch instead (using trunk vlan832)

Switch:
- Probably any

Media converter:
- MC220L v2.x
- MC220L v3.x
