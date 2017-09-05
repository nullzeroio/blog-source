---
title: 'PsTools - Auto Accept EULA'
slug: /pstools-auto-accept-eula/
date: 2011-12-14T13:44:13+00:00
author: Kevin Kirkpatrick
categories:
  - Scripting
tags:
  - PsTools
  - script command
  - Scripting
  - Windows
draft: false
---
When using or scripting anything from the PsTools suite it can sometimes be an inconvenience to have the EULA appear the first time you run any given tool on a system. In order to avoid this, simply append the  __`/accepteula`__ switch to your command and it will automatically accept and allow the script/command to run.

```
pslist /accepteula
```