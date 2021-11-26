---
layout: post
title: Accessing my self-hosted services away from home with WireGuard
description: 
summary: 
---

https://github.com/angristan/wireguard-install

```
curl -O https://raw.githubusercontent.com/angristan/wireguard-install/master/wireguard-install.sh
chmod +x wireguard-install.sh
./wireguard-install.sh
```

Run the script, enter the public IP for the server and leave everything else as default. Note the port it auto assigns.

Script will prompt to add the client name

Open the port to the internet, in my case on a TP-Link Archer router it was under a section called virtual servers