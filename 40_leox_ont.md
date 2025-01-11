---
layout: default 
title: LXE-010X-A
has_children: true
nav_order: 40
has_toc: false
---

# Introduction

The **Leox LXE-010X-A** is a budget-friendly external Optical Network Terminal (ONT) priced at approximately €120 (VAT and shipping included, late 2024). It connects to your router via a 10GbE copper (10GBASE-T) interface, offering great value despite its external design.

{: .important }
To bypass the Orange Livebox 7 without extra modifications, only the custom firmware **V4.2.4L6a3** is compatible.

# Compatibility

Routers must support the following to work with this ONT:
- VLAN mapping
- MAC address cloning
- DHCP options 60/77/90
- DHCP CoS

The ONT has been tested with a Ubiquiti Dream Wall (UniFi OS 4.0.20/Network 8.6.9) and should perform well with similar models, such as the UDM series or MikroTik CCR2004.