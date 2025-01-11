# MiniArch

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/donate/?hosted_button_id=XWV5VJH6L3DF6) for new HW support

Note: 
Last years I funded my semi-lab with 15+ various TVboxes by my private money and decided to stop investing my private money - effectively just (and seems only) - to increase sells of tv box vendors.

If you want me to work on various issues or add new hardware support - pls consider donation to help me get required hardware to work on.
Please note that this will also increase my satisfaction from - currently free of charge - work on minimyth2/miniarch.

## What it is

MiniArch is [ArchLinux ARM](https://archlinuxarm.org) set of SD card images offering plug&run ArchLinux on ARM SBC/TVbox.
It is very minimal ArchLinux distribution with bootloader/Linux kernel maximally supporting given TVBox/SBC then offering https://wiki.archlinux.org  

Currently supported (and tested) [SBC/TVboxes](https://github.com/warpme/minimyth2#current-status)

MiniArch artefact is part of following GAR based build ecosystem:

![alt text](https://github.com/warpme/minimyth2/blob/master/miniX_projects_overview.jpg?raw=true)

## Why MiniArch?

-Installing ArchLinux ARM on ARM SBC is currently multistep process ([example](https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-4))

MiniArch goal is to simplify above whole process to:
1. [Download](https://github.com/warpme/miniarch/releases) of MiniArch SD card image prepared for your SBC/TVbox
2. burn image on SD card
3. insert SD Card into SBC/TVbox
4. power-on
5. do update (see Quick Start below)
6. enjoy full ArchLinux capabilities

-Adding to ArchLinux ARM ecosystem MiniMyth2 developed support for [SBC/TVboxes](https://github.com/warpme/minimyth2#current-status) 
including [hardware video decode capabilities](https://github.com/warpme/minimyth2#hardware-video-decode-support)
(with following [results](https://github.com/warpme/minimyth2/blob/master/video-test-summary.txt))

## Quick Start
Requirements:
1. Make sure your box is connected to Eth, has IP and Internet access

### Install (when You will stay with SD Card) :
Note: pls do all below steeps in exact order like below. Otherwise install will fail! 

1. [Download]() SD card Image
2. burn image on SD card
3. insert SD Card into SBC/TVbox
4. power-on
5. do update
   - local login as root:root (ssh user:pass are alarm:alarm) 
   - type ```start```
     - select (1) to init keyring and key
   - type ```start```
     - select (2) to do full update
     - reboot
   - type ```start```
     - select (4) to resize root partition to full possible size
   - type ```start```
     - select (5) to update MiniArch artefacts
     - reboot
6. enjoy (i.e. install [EndeavourOS](https://arm.endeavouros.com) by typing ```start``` then (6) or setup ArchLinux OS acordingly to [Archlinux Wiki](https://wiki.archlinux.org/title/Installation_guide#Time_zone) 

### Install (when You will use eMMC as target) :
Note: pls do all below steeps in exact order like below. Otherwise install will fail! 

1. [Download]() SD card Image
2. burn image on SD card
3. insert SD Card into SBC/TVbox
4. power-on
5. do update
   - local login as root:root (ssh user:pass are alarm:alarm) 
   - type ```start```
     - select (1) to init keyring and key
   - type ```start```
     - select (2) to do full update
     - reboot
   - type ```start```
     - select (5) to update MiniArch artefacts
     - reboot
6. transfer system to eMMC
   - type ```start```
     - select (3)
     - when script ends with success, remove SD Card and reboot
7. Continue install
   - type ```start```
     - select (4) to resize root partition to full possible size
     - reboot
8. enjoy (i.e. install [EndeavourOS](https://arm.endeavouros.com) by typing ```start``` then (6) or setup ArchLinux OS acordingly to [Archlinux Wiki](https://wiki.archlinux.org/title/Installation_guide#Time_zone)


NOTE: do not skip step (update MiniArch artefacts) as this step - beside updating MiniArch components - also fixes bugs/issues/show stoppers in [Generic AArch64 ArchLinux ARM](https://archlinuxarm.org/platforms/armv8/generic) code

NOTE2: sometimes there are issues with Archlinux ARM mirrors avaliability. In such case do full update (option 2 in start) will be constantly failing. To overcome this You may change mirror to other one with hope other one will work better. In such case look on list of avaliable servers is here [list of mirrors](https://archlinuxarm.org/about/mirrors)
and do following:

#### Change mirror server for udates

On command prompt do:

(example for chnaging mirror to http://de3.mirror.archlinuxarm.org): 

```mv /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak```

```echo Server = 'http://de3.mirror.archlinuxarm.org/$arch/$repo' >> /etc/pacman.d/mirrorlist```

Verify Your change by:
```cat /etc/pacman.d/mirrorlist```

Try again with update by ```start 2```

## Difference between ArchLinux ARM and MiniArch

Currently automated MiniArch build process is following:
1. cross building current mainline Linux kernel and firmware with MiniMyth2 applied patches to offer [support of](https://github.com/warpme/minimyth2#current-status) SBC/TVboxes
2. cross-building selected SBC/TVbox bootloader files
3. cross-building ArchLinux kernel and firmware PKGs from p.1
4. downloading ArchLinux ARM [Generic AArch64 ArchLinux ARM](https://archlinuxarm.org/platforms/armv8/generic) rootfs
5. unpacking rootfs from p.4 on x86 host
6. cross-installing ArchLinux kernel and firmware PKGs generated in p.3 on unpacked rootfs from p.5 on x86 host
7. cross-regenrating initramfs on rootfs from p.6
8. packing above rootfs to Generic AArch64 Installation archive for upload to MiniArch github
9. preparing SD card image with updated rootfs and bootloader prepared in p.2 and p.7
10. xz packing SD card image for upload to MiniArch github

In above context, we may say: MiniArch is minimally required changed ArchLinux ARM to boot and work on Your box and it offers maximum compatibility with ArchLinux ARM (except kernel modules).

## ArchLinux ARM and MiniArch updates
MiniArch specific components are:
- linux-aarch64
- linux-aarch64-headers
- linux-aarch64-api-headers
- linux-firmware
- miniarch-meta

Above packages are blocked in ArchLinux ARM pacman official repo updates and are separately updated from dedicated repo called MiniArch

Any MiniMyth2 kernel update will also produce updated above PKGs.

You can update MiniArch kernel/firmware/meta by:
 - login as root:root
 - type 'start'
   - select (5) to do "update MiniArch artefacts"

Happy burning!

## Building / developing MiniArch

For building / developing MiniArch - pls go to: [building wiki](https://github.com/warpme/miniarch/wiki/Building-MiniArch) or [developing wiki](https://github.com/warpme/miniarch/wiki/Developing-MiniArch)
