---
layout: post
title: Setting up WSL to sidestep a corporate network
description: 
summary: 
---

WSL2 refuses to check the SSL certificates of any download locations, e.g. apt, pypi, github, vs code server, when on a corporate network

The only way to sidestep this as a permanent fix is to disable SSL checks on utilities that need to perform these downloads

In the case of VS Code server, create the file `~/.wgetrc` and add the following line

```
check_certificate = off
```

For Apt, create the file `~/.curlrc` and add the following line

```
insecure
```

And for PyPi, create the file `~/.config/pip/pip.conf` and add the folloiwng line

```
[global]
trusted-host = pypi.python.org
               pypi.org
               files.pythonhosted.org
```

And for GitHub, run the below config command:

```
git config --global http.sslverify false
```

All done. Insecure as hell, but it works!