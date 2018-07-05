---
title:  "Recover Disk Space in MacOS via Terminal"
search: false
categories:
  - Terminal
  - MacOS
last_modified_at: 2018-07-05 02:53:54

---

I've been reading more posts on r/mac and r/macOS of fellow users attempting to recover granular disk space. Here's a short snippet on how to reclaim some space from your Mac.

<!--more-->

Open the Terminal by pressing `⌘+SPACE` and type `Terminal` in Spotlight. Type `df -h` to list out your mounts.

    $ df -h

We are looking for the startup disk, which is mounted under **root**. My available space is 39GB. Let's see what I can recover.

    $ df -h
    Filesystem      Size   Used  Avail Capacity     iused               ifree %iused  Mounted on
    /dev/disk1s1   113Gi   72Gi   39Gi    66%     1468966 9223372036853306841    0%   /

If you're unsure about the mount, you can verify your startup disk by using Disk Utility under System Preferences. See below for an example.

![Disk space]({{ site.url }}{{ site.baseurl }}/assets/images/disk-space.png)

Next type `sudo du -xskh /* | sort -rn | head` to get a list of directories with their respective sizes. The main culprits are normally **/Users** and **/Applications**. In my case the **Users** seems to be quite large.

    $ sudo du -xskh /* | sort -rn | head  
    23G	/Users
    21G	/Applications
    10G	/System
    5.5K	/dev
    4.0K	/Volumes
    3.6G	/private
    2.5M	/bin
    2.4G	/usr
    2.4G	/Library
    1.0M	/sbin

Type `cd /Users/[username]` to switch to your user directory. Run the command `sudo du -xskh ./* | sort -rn | head`. You will get a breakdown of your users directory.

    $ sudo du -xskh ./* | sort -rn | head  
    912K	./Applications
    780K	./Music
    256M	./Documents
    236K	./Downloads
    228M	./Movies
    110M	./git
     24K	./Desktop
     17G	./Library
     13M	./PycharmProjects
    4.8G	./Pictures

I have a sizable amount of pictures in my **Pictures** directory. MacOS does not display this data when running `Manage Storage` on the startup disk, as you can see below. The culprit was the Apple Photos `Library.photoslibrary` file. This is a relatively simple fix as I can move the Photos Library to my external SSD drive.

![Disk space]({{ site.url }}{{ site.baseurl }}/assets/images/manage-storage.png)
