---
title:  "Find Hidden Files in MacOS"
search: false
categories:
  - Terminal
  - MacOS
last_modified_at: 2018-08-02 01:19:52

---

Here's a quick guide on how to find a hidden file or folder using the Terminal.

<!--more-->

Open the Terminal by pressing `⌘+SPACE` and type `Terminal` in Spotlight. Type `df -h` to list out your mounts.

    $ df -h

In this case we are looking for an external drive, which is mounted under **/Volumes/Data**. Let's see if I can find my folder named "Test".

    $ df -h
    Filesystem      Size   Used  Avail Capacity     iused               ifree %iused  Mounted on
    /dev/disk1s1   113Gi   75Gi   34Gi    70%     1533947 9223372036853241860    0%   /
    devfs          227Ki  227Ki    0Bi   100%         787                   0  100%   /dev
    /dev/disk1s4   113Gi  3.0Gi   34Gi     9%           3 9223372036854775804    0%   /private/var/vm
    map -hosts       0Bi    0Bi    0Bi   100%           0                   0  100%   /net
    map auto_home    0Bi    0Bi    0Bi   100%           0                   0  100%   /home
    map auto_nfs     0Bi    0Bi    0Bi   100%           0                   0  100%   /Users/abid/nfs
    drivefs         16Ti   16Ti   36Gi   100% 18446744069414585447          4294967295 1638254357852094720%   /Volumes/GoogleDrive
    /dev/disk3s1   931Gi   25Gi  906Gi     3%       18134 9223372036854757673    0%   /Volumes/Data

Type `cd /Volumes/Data` to change paths to your external drive. If you need to go deeper in your external drive, simply type `cd <folder name>` to drill down to the desired directory. Next, type `ls -la` to list all files and folder, including ones that are hidden.

    $ cd /Volumes/Data
    $ ls -la
    total 24
    drwxrwxr-x   9 abid  staff    288 Aug  2 01:30 .
    drwxr-xr-x@  5 root  wheel    160 Aug  2 01:49 ..
    -rw-r--r--@  1 abid  staff  10244 Aug  2 01:29 .DS_Store
    drwx------   5 abid  staff    160 Jul 17 13:36 .Spotlight-V100
    d-wx-wx-wt   3 abid  staff     96 Jul 17 13:39 .TemporaryItems
    drwxr-xr-x   3 abid  staff     96 Aug  2 01:18 .Test
    d-wx-wx-wt   3 abid  staff     96 Jul 19 03:26 .Trashes
    drwx------  13 abid  staff    416 Jul 30 01:26 .fseventsd
    drwxr-xr-x   5 abid  staff    160 Jul 17 13:42 Photos

Here, I can see my folder "Test" is present. Great! But how do we make it visible again? Simply type "mv .Test Test". This renames the hidden folder and renames it to a normal folder.

    $ mv .Test Test
    $ ls -la
    total 24
    drwxrwxr-x   9 abid  staff    288 Aug  2 01:58 .
    drwxr-xr-x@  5 root  wheel    160 Aug  2 01:49 ..
    -rw-r--r--@  1 abid  staff  10244 Aug  2 01:29 .DS_Store
    drwx------   5 abid  staff    160 Jul 17 13:36 .Spotlight-V100
    d-wx-wx-wt   3 abid  staff     96 Jul 17 13:39 .TemporaryItems
    d-wx-wx-wt   3 abid  staff     96 Jul 19 03:26 .Trashes
    drwx------  13 abid  staff    416 Jul 30 01:26 .fseventsd
    drwxr-xr-x   5 abid  staff    160 Jul 17 13:42 Photos
    drwxr-xr-x   3 abid  staff     96 Aug  2 01:18 Test

I can now see my folder in Finder.

![Hidden folder]({{ site.url }}{{ site.baseurl }}/assets/images/hidden-folder.png)
