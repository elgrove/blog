---
layout: post
title: Editing the sshd config file
description: 
summary: 
---

```
sudo nano /etc/ssh/sshd_config
```

Switch password authentication on/off

```
# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication no 
```

To reload the daemon and apply changes

```
sudo systemctl reload sshd
```
