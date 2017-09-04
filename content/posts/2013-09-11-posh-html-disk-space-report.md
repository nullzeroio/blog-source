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

```
<#
        HTML Server Disk Usage Report Script
        Kevin Kirkpatrick
        nullzero.io
        Created 7/31/2013

        This report, as currently written, is meant to create and save the HTML report in a location of your Choosing.
        If attaching the HTML report is desired, edit the EMail settings attachemtn location variable and go to the
        bottom of the script and un-comment the attachment options.
#>

# Custom HTML Report Formatting
$html = "<style>"
$html = $html + "BODY{background-color:White;}"
$html = $html + "TABLE{border-width: 1px;border-style: solid;border-color: black;border-collapse: collapse;}"
$html = $html + "TH{border-width: 1px;padding: 0px;border-style: solid;border-color: LightGrey;background-color:#F0E68C}"
$html = $html + "TD{border-width: 1px;padding: 0px;border-style: solid;border-color: LightGrey;background-color:#FAFAD2}"
$html = $html + "</style>"

# Script Variables
$Servers               = (gc "\\uncpath\to\servers.txt")
$ErrorActionPreference = "SilentlyContinue"
$SizeInGB              = @{Name = "Size(GB)"; Expression      = {"{0:N2}" -f ($_.Size/1GB)}}
$FreespaceInGB         = @{Name = "Freespace(GB)"; Expression = {"{0:N2}" -f ($_.Freespace/1GB)}}
$PercentFree           = @{name = "PercentFree(%)"; Expression={[int](($_.FreeSpace/$_.Size)*100)}}

#Email settings Variables
$Recipients = "report_recipients@company.com"
$Sender     = "ServerDiskReport@company.com"
$SMTPServer = "smtpserver.company.com"
#$AttachmentFile="\\uncpath\to\ServerDiskSpaceReport--$(( get-date ).ToString('yyyyMMdd')).html"

#Script Body
Write-Output "Gathering Disk Usage Information..."
gwmi -query "SELECT SystemName,Caption,VolumeName,Size,Freespace FROM win32_logicaldisk WHERE DriveType=3" -computer $Servers |
Select-Object SystemName,Caption,VolumeName,$SizeInGB,$FreespaceInGB,$PercentFree |
sort-object "PercentFree(%)" |
ConvertTo-Html -as table -head $html -body "<H2>Server Disk Space Report</H2>" |
Out-File "\\uncpath\to\ServerDiskSpaceReport--$(( get-date ).ToString('yyyyMMdd')).html"



# The attachment option has been commented out. Uncomment to enable attaching the HTML report to a message.
$smtpServer  = $SMTPServer
$msg         = new-object Net.Mail.MailMessage
#$att        = new-object Net.Mail.Attachment($AttachmentFile)
$smtp        = new-object Net.Mail.SmtpClient($smtpServer)
$msg.From    = $Sender
$msg.BCC.Add($Recipients)
$msg.Subject = "Server Disk Usage Report"
$msg.Body    = "The most recent Server Disk Space report has been posted at the following URL: http:// "
#$msg.Attachments.Add($att)
$smtp.Send($msg)
```

[img-report-demo-output]: https://raw.githubusercontent.com/nullzeroio/blog-source/master/static/public/img/report_demo_output.jpg