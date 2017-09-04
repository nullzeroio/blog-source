---
title: Nexus 1000v Max-Ports
date: 2011-12-14T21:15:54+00:00
author: Kevin Kirkpatrick
slug: /nexus-1000v-max-ports/
post_views_count:
  - "316"
categories:
  - Cisco 1000V
  - VMware
tags:
  - Cisco 1000V
  - Nexus
  - Nexus 1000v
  - port profile
  - port profiles
  - vlan
  - vmware max-ports
draft: false
---
I have been meaning to post something about this for a little while. When deploying the Nexus 1000v, don't forget to set the 'Max-Ports' setting for each of your port-profiles. By default, the 1000v sets each port-profile up with only 32 ports. This presents a problem, for example, when you try to deploy your 33rd guest and you get an error that says that you are out of virtual ports. Not to worry, the fix easy and non-disruptive to anything already running in your environment.

The syntax order looks like this:

```
conf t
port-profile type vethernet vmpublic_vlan
vmware max-ports 256
end
copy run start
```

You will see a reconfiguration task kick off in your vSphere client, that's about it; the change is instant. See below for a screen snip example.

![Example][img-1]

[img-1]: https://raw.githubusercontent.com/nullzeroio/blog-source/master/static/public/img/capture-3.jpg