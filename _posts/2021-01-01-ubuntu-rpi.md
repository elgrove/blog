---
layout: post
title: Installing 64-bit Ubuntu 20.04 on a Raspberry Pi
description: 
summary: 
---

```
wifis:
    wlan0:
        dhcp4: true
        optional: true
        access-points:
            "SSID":
                password: "PASS"
```


```
sudo apt install bluez pi-bluetooth

sudo reboot nowreboot

bluetoothctl

discoverable on
scan on 
pair 00:11:22:33:44:55
connect 00:11:22:33:44:55
```