---
title:  "DL380 Gen8 - Installing a USB 3.0 PCI-e card"
search: false
categories:
  - Proxmox
  - Hardware
last_modified_at: 2021-20-02 08:10:00

---

I was using a couple of USB 2.0 external hard drives on my DL380p Gen8 for backups. After performing an initial seed I decided I needed something faster - but the DL380p Gen8 isn't equipped with any USB 3.0 ports so I bought one from Amazon.

Did it work? No. Well...at least not at first.

<!--more-->

### Installing a USB 3.0 PCI-e card on a DL380p Gen8

I'm using Proxmox with the latest kernel, `5.4.86-1-pve` at the time of writing. I was unable to get the server to detect the USB 3.0 PCI-e card. I initiated a return with Amazon and opened up the server. Then I remembered that the DL380p Gen8 server has a single PCI-e 2.0 card. So I figured why not - let's try it!

![dl380p gen8 pcie 2.0 port]({{ site.url }}{{ site.baseurl }}/assets/images/dl380p_pcie2.png)

I booted it up and it mounted both my USB backup drives. I tested a transfer and I averaged ~19GB in 2.5 minutes. I'll take that over USB 2.0 speeds _any_ day.

![USB 3 Transfer]({{ site.url }}{{ site.baseurl }}/assets/images/usb3transfer.png)
