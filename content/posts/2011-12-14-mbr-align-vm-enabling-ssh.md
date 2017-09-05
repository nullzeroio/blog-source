---
title: 'MBR Align VM and Enabling SSH'
slug: /mbr-align-vm-enabling-ssh/
date: 2011-12-14T21:39:13+00:00
author: Kevin Kirkpatrick
categories:
  - Linux
  - NetApp
  - VMware
tags:
  - alignment
  - mbr
  - mbralign
  - NetApp
  - shell
  - ssh
  - Suse
  - vmdk
  - vmdk alignment
  - VMware
draft: false
---
I got real sick and tired of the left click getting stuck in my MBR Align guest, midway through a vmdk alignment. While I did see some fixes, all I really needed was SSH enabled so I could run the necessary utilities from the command line.

To enable SSH on the MBR Align Suse VM, do the following:

1. Open the shell

2. Enter the below command:
```
sudo /etc/rc.d/./sshd start
```

Thats it; done.