---
title: Leveraging PowerShell
slug: /leveraging-powershell/
date: 2011-09-22T12:46:44+00:00
author: Kevin Kirkpatrick
categories:
  - PowerShell
tags:
  - NetApp
  - PowerGUI
  - PowerShell
  - VMware
draft: false
---
While I am no seasoned veteran with PowerShell, I have been using it heavily for the past 6 months or so to help automate tasks and increase the speed of my system management workflow. I have recently noticed that not many admins that I have been talking to, in and out of my place of work, are really leveraging what it has to offer. I realized that looking at an example .ps1 (PowerShell) script really feels like a programming language and that is a turn off for most; "I am not a coder; this isn't for me."

However, most programming languages aren't diverse enough where you can go from entering a single line of code and immediately getting feedback in the shell all the way to creating a 1000+ line script that organizes and distributes a report. It's this diversity that really makes it useful; once you know the syntax you can simply fire up the shell, enter commands and get what you need OR script the process. With the demise of Server 2003 and XP, migrations to Windows 7 and Server 2008 R2 are full steam and PowerShell can really help you out. The operating systems themselves (Win 7 & Server 2008) are built entirely on top of PowerShell which means you can basically script anything you want.

The last point I will make is about PowerGUI. PowerGUI is a management interface where you can view and edit code as well as leverage various 'PowerPacks' to aid in management. There is a large community base and some really good tools that aid in system management including official PowerPacks from NetApp and the VMware Community. I will list some screen snips below. I could rant on about how cool it is but hopefully this piques your interest to take a look/review it again.

* [PowerShell Magazine Website][1]
* [PowerGUI Website][2]
* [Alan Renouf's Blog (Co-Auther of PowerCLI Reference Book)][3]
* [Learn Windows PowerShell in a Month of Lunches - Don Jones][4]


![VMware][img-1-vmware]
* * *
![Netapp][img-2-netapp]

[1]: http://bit.ly/nZibEn
[2]: http://bit.ly/qojKGJ
[3]: http://bit.ly/ocETit
[4]: http://bit.ly/oTTIPU
[img-1-vmware]: https://raw.githubusercontent.com/nullzeroio/blog-source/master/static/public/img/vmware.jpg
[img-2-netapp]: https://raw.githubusercontent.com/nullzeroio/blog-source/master/static/public/img/netapp.jpg