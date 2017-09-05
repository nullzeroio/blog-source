---
title: Testing Jumbo Frame Support on ESXi
slug: /testing-jumbo-frame-support-esxi/
date: 2017-09-05
author: Kevin Kirkpatrick
tags:
  - esxi
  - vmware
  - jumboFrames
  - mtu
draft: false
---
You will need to SSH into the host to perform these commands.

This is the basic syntax
```
vmkping -4 -d -I <vmk-number> -s <packet-size> <address>
```

* This is an example using vmk3 and vmk4, which we will assume is used for storage.
* We will use a packet size of 8400 bytes (can't use 9000 b/c there won't be enough room to allow for IP overhead)
* We will assume 192.168.1.10 is the address of the storage interface

```
vmkping -4 -d -I vmk3 -s 8400 192.168.1.10

vmkping -4 -d -I vmk4 -s 8400 192.168.1.10
```

* Make sure you test all interfaces from the host, against all hosted ip addresses on the storage



