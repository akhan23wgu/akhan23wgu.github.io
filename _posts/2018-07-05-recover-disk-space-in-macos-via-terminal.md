---
title:  "Recover Disk Space in MacOS via Terminal"
search: false
categories:
  - Terminal
  - MacOS
last_modified_at: 2018-07-05 02:53:54

---

I've been reading more and more posts on r/mac and r/macOS of fellow users attempting to recover granular disk space. Here's a short snippet on how to reclaim some space from your Mac.

<!--more-->

Open up Terminal by pressing `⌘+T` or typing `Terminal` in Spotlight.

    df -h

Type `df -h` to list out your mounts. We are looking for the startup disk, which is mounted under **root**. My available space is 39GB.

    Filesystem      Size   Used  Avail Capacity     iused               ifree %iused  Mounted on
    /dev/disk1s1   113Gi   72Gi   39Gi    66%     1468966 9223372036853306841    0%   /

If you're unsure about the mount, you can verify your startup disk by using Disk Utility under System Preferences. See below for an example.

![Disk space]({{ site.url }}{{ site.baseurl }}/assets/images/disk-space.png)
