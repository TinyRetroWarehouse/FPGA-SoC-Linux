### DE0-Nano-SoC

#### Downlowd from github

```
shell$ git clone git://github.com/ikwzm/FPGA-SoC-Linux
shell$ cd FPGA-SoC-Linux
shell$ git lfs pull origin master
```

#### File Description

 * target/de0-nano-soc/
   + boot/
     - DE0_NANO_SOC.rbf                                            : FPGA configuration file (Raw Binary Format)
     - uEnv.txt                                                    : U-Boot environment variables for linux boot
     - zImage-4.12.13-armv7-fpga                                   : Linux Kernel Image       
     - devicetree-4.12.13-socfpga.dtb                              : Linux Device Tree Blob   
     - devicetree-4.12.13-socfpga.dts                              : Linux Device Tree Source
   + u-boot/
     - u-boot-spl.sfp                                              : Stage 1 Boot Loader(U-boot-spl)
     - u-boot.img                                                  : Stage 2 Boot Loader(U-boot)
   + examples/                                                     : Example Programs
 * debian8-rootfs-vanilla.tgz                                      : Debian8 Root File System (use Git LFS)
 * linux-image-4.12.13-armv7-fpga_4.12.13-armv7-fpga-1_armhf.deb   : Linux Image Package
 * linux-headers-4.12.13-armv7-fpga_4.12.13-armv7-fpga-1_armhf.deb : Linux Headers Package
 * fpga-soc-linux-drivers-4.12.13-armv7-fpga_0.0.7-1_armhf.deb     : Device Drivers Package 
 * fpga-soc-linux-services_0.0.7-1_armhf.deb                       : Device Services Package

#### Format SD-Card

````
shell# fdisk /dev/sdc
   :
   :
   :
shell# mkfs-vfat /dev/sdc1
shell# mkfs.ext3 /dev/sdc2
````

#### Write to SD-Card

````
shell# mount /dev/sdc1 /mnt/usb1
shell# mount /dev/sdc2 /mnt/usb2
shell# cp target/de0-nano-soc/boot/* /mnt/usb1
shell# dd if=target/de0-nano-soc/u-boot/u-boot-spl.sfp of=/dev/sdc3 bs=64k seek=0
shell# dd if=target/de0-nano-soc/u-boot/u-boot.img     of=/dev/sdc3 bs=64k seek=4
shell# tar xfz debian8-rootfs-vanilla.tgz -C                              /mnt/usb2
shell# cp linux-image-4.12.13-armv7-fpga_4.12.13-armv7-fpga-1_armhf.deb   /mnt/usb2/home/fpga
shell# cp linux-headers-4.12.13-armv7-fpga_4.12.13-armv7-fpga-1_armhf.deb /mnt/usb2/home/fpga
shell# cp fpga-soc-linux-drivers-4.12.13-armv7-fpga_0.0.7-1_armhf.deb     /mnt/usb2/home/fpga
shell# cp fpga-soc-linux-services_0.0.7-1_armhf.deb                       /mnt/usb2/home/fpga
shell$ cp -r target/de0-nano-soc/examples                                 /mnt/usb2/home/fpga
shell# umount mnt/usb1
shell# umount mnt/usb2
````
