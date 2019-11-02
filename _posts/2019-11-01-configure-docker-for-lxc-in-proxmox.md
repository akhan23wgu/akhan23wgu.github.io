---
title:  "Configure Docker for LXC in Proxmox"
search: false
categories:
  - Docker
  - Proxmox
  - LXC
last_modified_at: 2019-11-01 10:54:00

---

Using Docker inside LXC can be challenging, but here's what works for me. A few gotcha's about my setup is that it is _not_ being used for production use, and I would  not recommend it.  I am using ZFS storage for my Linux Container, this will mean this setup may not work if you're using NFS or LVM storage configuarations.

<!--more-->

### Configure Docker for LXC

Install docker-ce on Ubuntu 19.04 LXC container and add $USER to `docker` group

    $ apt-get install docker-ce
    $ usermod -aG docker $USER

Modify `/etc/modules-load.d/modules.conf`

    aufs
    vfs

Modify `/etc/docker/daemon.json`
 - This is needed because I am using ZFS storage. If you are using LVM, I would imagine overlay2 would work just fine.
   
    {
      "storage-driver": "vfs"
    }

Run `systemctl daemon-reload && systemctl start docker`
Setup Docker-Compose network
 - [See official Docker documentation on how to configure your network](https://docs.docker.com/network/macvlan/)
Run `docker-compose up -d`
 - If receiving HTTP errors, restart docker and run again. You may need to adjust your timeouts appropriately.
Additional parameters for lcx 1xx.conf in `/opt/pve/lxc/`

    lxc.cgroup.devices.allow: a
    lxc.mount.auto: proc:rw sys:rw
    lxc.cap.drop: 
    features: nesting=1
    
Configure mountpoints (optional)
 
    mp0: /zstorage/media,mp=/zstorage/media
    mp1: /zstorage/home,mp=/zstorage/home
    mp2: /zstorage/timemachine,mp=/zstorage/timemachine

### Sources
(Proxmox Forum: Docker in lxc container](https://forum.proxmox.com/threads/docker-in-lxc-container.45204/)
