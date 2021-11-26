---
layout: post
title: LAN Speed Testing with iperf
description: 
summary: 
---

`iperf` is a command line tool for \*nix machines that can set up a server-client connection over the LAN to transfer as much data as possible in ten seconds flat, and thus measure the speed of the connection.

Using this tool I found out that my 5GHz wifi band (370Mbps) is three times faster than the TP-Link powerline tool (93Mbps) I had been using previously, and a massive 23x faster than the 2.4GHz band (16Mbps)!

I think this is in large part due to the TP-Link Archer C2300 router I bought when we moved in, it was only £90 and is a huge upgrade on whatever your ISP gave you.

```bash
# linux
sudo apt install iperf
# macos
brew install iperf

# on server
iperf -s

# on client
iperf -c 10.0.0.x -p port