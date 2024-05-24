---
layout: default 
title: ONU verification
parent: XGS-ONU-25-20NI
has_children: false
nav_order: 22
has_toc: false
---

# Verification


## Vendor, serial, hardware version

```
./fs_xgspon_mod.py telnet SMBSXXXXXXXX
```
> Where `SMBSXXXXXXXX` is the livebox serial

then

```
/s/m/show 256
/s/m/show 257
```
These two commands should make it possible to display the serial, vendor and hardware version to verify the correct values ​​(in hex).


## Reg status

```
/traffic/pon/show onu
```
> ------------------------- ONU INFO --------------------------
>
> Onu id 26
>
> sdThreshold:   0
>
> sfThreshold:   0
>
> TO1:   80000
>
> TO2:   1
>
> eqd:   XXXXXXXX
>
> Serial Number(vendor code): SMBS
>
> Serial Number(sn):          XXXXXXX
>
> Password:                   XX XX XX XX XX XX XX XX XX XX
>
> Registration ID:           0xXXXXXXXXXXXXXXXX0000000000000000000000000000000000000000000000000000000000
>
> ------------------------- INFO END --------------------------


## Status O5

```
/traffic/pon/show link
```
> ----------------- LINK STATE -----------------
>
> Operation State Machine: OPERATION (O5)
>
> ----------------- STATE  END -----------------


## VLAN

```
/system/mib/show 506
```

> EntityID                  = 0x0101
>
> OuterPriFilter            = 15
>
> OuterVidFilter            = 4096
>
> OuterTPIDFilter           = 0
>
> InnerPriFilter            = 8
>
> InnerVidFilter            = 832
>
> InnerTPIDFilter           = 5
>
> EtherTypeFilter           = 0
>
> AniBriPortNum             = 2
>
> RmTagTreat                = 1
>
> OuterPriTreat             = 15
>
> OuterVidTreat             = 0
>
> OuterTPIDTreat            = 0
>
> InnerPriTreat             = 8
>
> InnerVidTreat             = 2800
>
> InnerTPIDTreat            = 2

> EntityID                  = 0x0101
>
> OuterPriFilter            = 15
>
> OuterVidFilter            = 4096
>
> OuterTPIDFilter           = 0
>
> InnerPriFilter            = 8
>
> InnerVidFilter            = 835
>
> InnerTPIDFilter           = 5
>
> EtherTypeFilter           = 0
>
> AniBriPortNum             = 6
>
> RmTagTreat                = 1
>
> OuterPriTreat             = 15
>
> OuterVidTreat             = 0
>
> OuterTPIDTreat            = 0
>
> InnerPriTreat             = 8
>
> InnerVidTreat             = 835
>
> InnerTPIDTreat            = 2

> ...


## VLAN Mapping

```
/traffic/eth/show connect all
```

> US BRIDGE 65535
>
> ---------------------------------------------------------------
>
> INDEX = 0, SLOT = 1, PORT = 4, VLANFILTER = 832 PRIFILTER = 0x1
>
>     VLAN MATCH : MATCH
>
>     VLAN ACT   : REPLACE
>
>     OUT  VID   : 2800
>
>     OUT  PRI   : 0
>
>     TCI MAPPING:
>
>                 * PRI 0  -> FLOW 1
>
>                 * PRI 1  -> FLOW 0
>
>                 * PRI 2  -> FLOW 0
>
>                 * PRI 3  -> FLOW 0
>
>                 * PRI 4  -> FLOW 0
>
>                 * PRI 5  -> FLOW 0
>
>                 * PRI 6  -> FLOW 0
>
>                 * PRI 7  -> FLOW 0