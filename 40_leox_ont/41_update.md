---
layout: default 
title: ONT Firmware Update
parent: LXE-010X-A
has_children: false
nav_order: 41
has_toc: false
---


# Getting ready

## Download firmware

Get the [V4.2.4L6a3 firmware](https://leox.pages.dev/V4.2.4L6a3) (hash: `724e0b9981c8b777d87b5c0992c31c46003bfedd4561c3ef31ee31fdacd4bf4`)

## Set up connectivity

The ONT is accessible at `192.168.100.1`. Configure your router with a VLAN using the `192.168.100.0/24` subnet and connect the ONT to a VLAN-mapped port.

This [existing guide](https://stoufiler.github.io/isp/bypass-livebox/) shows how to do this on a Ubiquiti router.


## ONT credentials

Note that there are different credentials for Web UI vs. command line:
- **Web UI** (HTTP): `admin`:`letmein`
- **Shell** (Telnet): `leox`:`leolabs_7`

We use the Web UI for the firmware update, and later will use shell access to update the ONT settings.

# Updating the firmware

{: .important }
Ensure the `HW_HWVER` value is set to `LXE-010X-A` (default). If changed to `SMBSxxxxxxx` for Livebox 7, revert it to `LXE-010X-A` before proceeding.

Steps
- Go to [http://192.168.100.1/upgrade.asp](http://192.168.100.1/upgrade.asp).
- Upload the `V4.2.4L6a3` file and confirm.
- After ONT reboot, verify the version at [http://192.168.100.1/status.asp](http://192.168.100.1/status.asp). It should show `V4.2.4L6a3`.