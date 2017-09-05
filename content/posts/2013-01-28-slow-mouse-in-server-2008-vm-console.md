---
title: Slow Mouse in Server 2008 VM Console
slug: /slow-mouse-in-server-2008-vm-console/
date: 2013-01-28T22:51:10+00:00
author: Kevin Kirkpatrick
tags:
  - Server 2008
  - Server 2008 R2
  - Slow mouse in VM console
  - VMware
draft: false
---
A while back I created a note about how to fix the slow mouse issue that sometimes happens even after installing VMware tools on a Server 2008 guest. The process is as follows:

**1.** Make sure VMware tools is up to date

**2.** You may need to update the VM hardware versions if this fix does not work.

**3.** On the guest, open up the device manager and expand the Display adapters.

**4.** Right click on Standard VGA Graphics Adapter and select Properties

**5.** Click the Driver tab.

**6.** Click the Update Driver button

**7.** Select Let me pick from a list of device drivers on my computer

**8.** Click have Disk button

**9.** Click browse and go to:

```
C:Program FilesCommon FilesVMwareDriverswddm_video
```

**10.** Select vm3d and click open.

**11.** Click OK on the Install From Disk window

**12.** VMware SVGA 3D (Microsoft Corporation - WDDM) should be selected

**13.** Click Next and then Close

**14.** A reboot is required so select Yes.

**15.** You may also need to adjust your display acceleration to "full".