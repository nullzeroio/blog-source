---
title: PowerShell HTML Disk Space Report
date: 2013-09-11T23:57:58+00:00
author: Kevin Kirkpatrick
slug: /posh-html-disk-space-report/
categories:
  - PowerShell
tags:
  - HTML
  - PowerShell
  - PowerShell Report
  - Scripting
  - Server Disk Space
draft: false
---
This is a recent HTML Disk Space report that I created which outputs a generic HTML report that contains server disk/partition space details. I schedule it to run weekly, but obviously you can use as you wish. In short, in reads in a list of servers from a text file, queries WMI for disk space detail, uses some expressions to format and calculate the space and then outputs the results into a report, sorted in ascending order by the percent of free space, per partition. Sample output, below.

![Demo Output][img-report-demo-output]

<script src="https://gist.github.com/vScripter/976b02c4b4cd3cbc20a255369713662c.js"></script>

[img-report-demo-output]: https://raw.githubusercontent.com/nullzeroio/blog-source/master/static/public/img/report_demo_output.jpg