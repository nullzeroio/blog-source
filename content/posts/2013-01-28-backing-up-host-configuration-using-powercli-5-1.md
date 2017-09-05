---
title: Backing Up Host Configuration using PowerCLI
slug: /backing-up-host-configuration-using-powercli-5-1/
date: 2013-01-28T22:29:16+00:00
author: Kevin Kirkpatrick
categories:
  - VMware
tags:
  - Backup
  - ESXi
  - Host Configuration
  - PowerCLI
  - VMware
  - vSphere-5.1
draft: false
---
An often overlooked and less prioritized thought in vSphere environments is backing up the actual host configuration. I figured it was worth a quick post, given the fact that it's a fairly simple process via PowerCLI. This command should be the same for all versions of vSphere/PowerCLI, but I have only tested on 4.1-5.1.

_Aside: This is just the basic command; there are plenty of other ways to automate this or use it in conjunction with another PowerCLI script; I'll leave that up to you._

1. Fire up PowerCLI

2. Connect to your vCenter server:

3. Expand the screen shot below to view the full command. The output will be a gzipped tar file in the location that you specify.

<script src="https://gist.github.com/vScripter/bf292f673a5092f8859cc6ec1f3982b4.js"></script>

![Host Backup][img-1]

[img-1]: https://raw.githubusercontent.com/nullzeroio/blog-source/master/static/public/img/powerclihostbackup.png