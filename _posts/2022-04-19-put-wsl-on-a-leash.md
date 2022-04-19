---
layout: post
title: Put WSL on a leash
---

![](/assets/images/wsl-on-a-leash.jpg){: .center-image }

For last few days, my laptop has been sluggish. So I checked the task manager to see what's happening and I found out that there is a process called `Vmmem` that is consuming around 8GB of memory. `Vmmem` is a virtual process on which virtual machines are run in Windows but I am not running any VMs so why is this process running? It turns out that Windows Subsystem for Linux (WSL), under the hood, is a VM and by default half of the total system memory will be available for consumption to it. 

There is an open [issue](https://github.com/microsoft/WSL/issues/4166) in WSL since 2019 related to this i.e. WSL consumes massive amount of memory and doesn't return it. The workaround to this problem is to put WSL on a leash by creating `%userprofile%/.wslconfig` and set the memory limit on WSL like this:

```
[wsl2]
memory=2GB
```