Upgrade to v1.3.0 from v1.0.x/v1.1.x/v1.2.x
------------------------------------------------------------------------------------

### Boot and login root user

fpga'password is "fpga".

```console
debian-fpga login: fpga
Password:
fpga@debian-fpga:~$
```

root'password is "admin".

```console
debian-fpga login: root
Password:
root@debian-fpga:~#
```

### Download FPGA-SoC-Linux v1.3.0

```console
root@debian-fpga:~# git clone --depth=1 --branch v1.3.0 git://github.com/ikwzm/FPGA-SoC-Linux
root@debian-fpga:~# cd FPGA-SoC-Linux
root@debian-fpga:~/FPGA-SoC-Linux# git lfs pull
```

### Backup /mnt/boot/uEnv.txt

```console
root@debian-fpga:~/FPGA-SoC-Linux# cp /mnt/boot/uEnv.txt /mnt/boot/uEnv.txt.org
```

### Install files for Booting

#### ZYBO

```console
root@debian-fpga:~/FPGA-SoC-Linux# cp target/zynq-zybo/boot/*    /mnt/boot
```

#### PYNQ

```console
root@debian-fpga:~/FPGA-SoC-Linux# cp target/zynq-pynqzq/boot/*  /mnt/boot
```

#### ZYBO-Z7

```console
root@debian-fpga:~/FPGA-SoC-Linux# cp target/zynq-zybo-z7/boot/* /mnt/boot
```

#### DE0-Nano-SoC

```console
root@debian-fpga:~/FPGA-SoC-Linux# cp target/de0-nano-soc/boot/* /mnt/boot
```

#### DE10-Nano

```console
root@debian-fpga:~/FPGA-SoC-Linux# cp target/de10-nano/boot/* /mnt/boot
```

### Setup /mnt/boot/uEnv.txt

If /mnt/boot/uEnv.txt.org has its own settings, please reflect it in the new /mnt/boot/uEnv.txt.

### Copy Debian Packages to /home/fpga/debian

```console
root@debian-fpga:~/FPGA-SoC-Linux# cp *.deb /home/fpga/debian
```

### Install Kernel Image and Device Drivers

[doc/install/device-drivers.md](device-drivers.md)


