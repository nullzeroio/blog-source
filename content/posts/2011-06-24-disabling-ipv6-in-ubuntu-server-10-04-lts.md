---
title: Disabling IPv6 In Ubuntu Server 10.04 LTS
slug: /disabling-ipv6-in-ubuntu-server-10-04-lts/
date: 2011-06-24T02:03:06+00:00
author: Kevin Kirkpatrick
tags:
  - 10.04 Server
  - IPv6
  - Linux
  - Lucid Lynx
draft: false
---
### Step 1
Run the following command to verify if it is enabled or disabled. _0=enabled & 1=disabled_
```
cat /proc/sys/net/ipv6/conf/all/disable_ipv6
```

### Step 2
Using __`vi`__ add the following lines to __`/etc/sysctl.conf`__

_the # comment is optional but considered a best practice_

```
#disable ipv6 
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1
```

###  vi Notes
|Command|Function
|:------:|:------
|__`i`__ | Enters __`insert`__ mode _(editing)_
|__`esc`__| exits __`insert`__ mode
|__`:`__ |followed by __`x`__ saves your work and exits

Reboot and run the first command to verify that is has been disabled.

### Compiled Code Example

<script src="https://gist.github.com/vScripter/bbc4ca2bbd7e9d4a190bbd6cb1777977.js"></script>