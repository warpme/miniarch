# MiniArch

[![Donate](https://img.shields.io/badge/Donate-PayPal-green.svg)](https://www.paypal.com/donate/?hosted_button_id=XWV5VJH6L3DF6) for new HW support

## What it is

MiniArch is [ArchLinux ARM](https://archlinuxarm.org) set of SD card images offering plug&run ArchLinux on ARM SBC/TVbox.

Currently supported (and tested) [SBC/TVboxes](https://github.com/warpme/minimyth2#current-status)

## Why MiniArch?

-Installing ArchLinux ARM on ARM SBC is currently multistep process ([example](https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-4))

MiniArch goal is to simplify above whole process to:
1. [Download](https://github.com/warpme/miniarch/releases) of MiniArch SD card image prepared for your SBC/TVbox
2. burn image on SD card
3. insert SD Card into SBC/TVbox
4. power-on
5. do update (see Quick Start below)
6. enjoy full ArchLinux capabilities

-Offer for ArchLinux ARM ecosystem MiniMyth2 developed support for [SBC/TVboxes](https://github.com/warpme/minimyth2#current-status) 
including [hardware video decode capabilities](https://github.com/warpme/minimyth2#hardware-video-decode-support)
(with following [results](https://github.com/warpme/minimyth2/blob/master/video-test-summary.txt))

## Quick Start

1. [Download]() SD card Image
2. burn image on SD card
3. insert SD Card into SBC/TVbox
4. power-on
5. do update
   - login as root:root
   - type 'start'
     - select (1) to do full update
   - type 'start'
     - select (2) to init keyring and keys
     - reboot
   - type 'start'
     - select (3) to resize root partition to full possible size
   - type 'start'
     - select (4) to update MiniArch artefacts
     - reboot
6. enjoy

## Difference between ArchLinux ARM and MiniArch

Currently automated MiniArch build process is following:
1. cross building current mainline Linux kernel and firmware with MiniMyth2 applied patches to offer [support for](https://github.com/warpme/minimyth2#current-status)
2. cross building selected SBC/TVbox bootloader files
3. building ArchLinux kernel and firmware PKGs from p.1
4. downloading ArchLinux ARM [Generic AArch64 Installation](https://archlinuxarm.org/platforms/armv8/generic)
5. unpacking rootfs from p.4
6. installing ArchLinux kernel and firmware PKGs generated in p.3 on unpacked rootfs from p.5
7. cross-regenrating initramfs on rootfs from p.6
8. packing above rootfs to Generic AArch64 Installation archive for upload to MiniArch github
9. prepare SD card image with updated rootfs and bootloader prepared in p.2 and p.7
10. xz pack SD card image for upload to MiniArch github

In above context, we may say: MiniArch is minimally required changed ArchLinux ARM and it should offer maximum compatibility with ArchLinux ARM.

## Updates
MiniArch specific components:
- linux-aarch64
- linux-aarch64-headers
- linux-aarch64-api-headers
- linux-firmware
- miniarch-meta

are blocked in ArchLinux ARM pacman official repo updates and are separately offered in dedicated repo called MiniArch

Any MiniMyth2 kernel update will also produce updated above PKGs.

You can update MiniArch with kernel/firmware by:
 - login as root:root
 - type 'start'
   - select (5) to do "updating MiniArch speciffic components"

Happy burning!
