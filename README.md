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
   - type 'start'
     - select (2) to init keyring and key
   - type 'start'
     - select (1) to do full update
     - reboot
   - type 'start'
     - select (3) to resize root partition to full possible size
   - type 'start'
     - select (4) to update MiniArch artefacts
     - reboot
6. enjoy (i.e. install https://arm.endeavouros.com by typing 'start' then (5) or setup ArchLinux OS acordingly to https://wiki.archlinux.org/title/Installation_guide#Time_zone) 

### Install (when You will use eMMC as target) :
Note: pls do all below steeps in exact order like below. Otherwise install will fail! 

1. [Download]() SD card Image
2. burn image on SD card
3. insert SD Card into SBC/TVbox
4. power-on
5. do update
   - local login as root:root (ssh user:pass are alarm:alarm) 
   - type 'start'
     - select (2) to init keyring and key
   - type 'start'
     - select (1) to do full update
     - reboot
   - type 'start'
     - select (4) to update MiniArch artefacts
     - reboot
6. transfer system to eMMC
   - type 'start'
     - select (0)
     - when script ends with success, remove SD Card and reboot
7. Continue install
   - type 'start'
     - select (3) to resize root partition to full possible size
     - reboot
8. enjoy (i.e. install https://arm.endeavouros.com by typing 'start' then (5) or setup ArchLinux OS acordingly to https://wiki.archlinux.org/title/Installation_guide#Time_zone) 


NOTE: do not skip step (update MiniArch artefacts) as this step - beside updating MiniArch components - also fixes bugs/issues/show stoppers in [Generic AArch64 ArchLinux ARM](https://archlinuxarm.org/platforms/armv8/generic) code
NOTE2: eMMC install is experimental feature and is not stable (yet)

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
   - select (4) to do "update MiniArch artefacts"

Happy burning!

## Building MiniArch
MiniArch is just another project (like MiniMyth2) living in build system MiniMyth2 uses. For some background - please look https://github.com/warpme/minimyth2/wiki/Build-Instructions

### Quick start
 
1. setup build system by following minimyth2 build instructions from https://github.com/warpme/minimyth2/wiki/Build-Instructions till ```cd ~/minimyth2/script/meta/minimyth/```
2. instead of ```cd ~/minimyth2/script/meta/minimyth/``` do ```cd ~/minimyth2/script/meta/miniarch/```
3. run ```./build-image-for-board.sh```
4. type number to select desired board then press Enter
5. after some time Yuo should got sd card image for selected board in ```build``` dir
6. flash to sd card. it should work ok

### Developing MiniArch
MiniArch (the same like MiniMyth2) uses common build system based on GAR (https://www.linuxjournal.com/article/5819)

Most frequently actions are described here: https://github.com/warpme/minimyth2/wiki/Developing-MiniMyth2

MiniArch related components are in ```~/minimyth2/script/miniarch```

#### Example: rebuilding MiniArch image with updated kernel
1. go to ```~/minimyth2/script/kernel/linux-x.y/work/main.d/linux-x.y.z```
2. do desired changes in kernel code
3. go to ```~/minimyth2/script/kernel/linux-x.y```
4. run ```make rebuild reinstall```
5. go to ```~/minimyth2/script/miniarch```
6. run ```make update-kernel```
7. run ```./build-image-for-board.sh```
4. type number to select desired board then press Enter
5. after some time You should get sd card image for selected board in ```build``` dir

Note: running make clean in ```~/minimyth2/script/kernel/linux-x.y``` will delete all your changes. If you want to have them permanently, please do following:

#### Include your code changes in MiniMyth2 build system
Here is example for linux kernel:
1. go to ```~/minimyth2/script/kernel/linux-x.y```
2. run ```make clean patch```
3. do desired changes in kernel code in ```~/minimyth2/script/kernel/linux-x.y/work/main.d/linux-x.y.z```
4. run ```make makepatch``` in ```~/minimyth2/script/kernel/linux-x.y``` 
5. you will get ```current-changes.patch``` file in ```~/minimyth2/script/kernel/linux-x.y```
copy this file to ```~/minimyth2/script/kernel/linux-x.y/files``` dir with desired *patch_file_name*
6. add ```PATCHFILES += patch_file_name``` entry in ```~/minimyth2/script/kernel/linux-x.y/Makefile``` at end of *PATCHFILES +=...* list
7. go to ```~/minimyth2/script/kernel/linux-x.y``` and run ```make makesums-all```

Now you can build kernel with your changes by ```make clean install``` and then build MiniArch image by following Example: rebuilding MiniArch image with updated kernel

Note: due nature how ```patch``` utility works - please do ```make makepatch``` on clean sources. 
If you do this on sources with build artefacts - then ```current-changes.patch``` file will contain also build artefacts. 
To avoid this, you may do whole *Include your code changes in MiniMyth2 build system* procedure in some temp dir.

Example:
1. copy ```~/minimyth2/script/kernel/linux-x.y``` to ```~/minimyth2/script/kernel/linux-x.y-temp```
2. go to ```~/minimyth2/script/kernel/linux-x.y-temp``` and do *Include your code changes in MiniMyth2 build system* procedure
3. copy ```current-changes.patch``` file from ```~/minimyth2/script/kernel/linux-x.y-temp```
to ```~/minimyth2/script/kernel/linux-x.y/files``` dir with desired *patch_file_name*
4. add ```PATCHFILES += patch_file_name``` entry in ```~/minimyth2/script/kernel/linux-x.y/Makefile``` at end of *PATCHFILES +=...* list
5. go to ```~/minimyth2/script/kernel/linux-x.y``` and run ```make makesums-all```    

Happy building
