# A64-Multimedia-boards
## General Instructions
The uboot and kernel device tree files are available for download , either as a patch or as individual files.
for compiling , follow below instructions.

TESTED on Ubuntu 22.04

```sh
apt-get install gcc-arm-linux-gnueabihf gcc-aarch64-linux-gnu flex bison swig python3-dev device-tree-compiler git libncurses-dev python3-setuptools libssl-dev pip2 pip
pip install pyelftools


git clone https://github.com/ARM-software/arm-trusted-firmware.git
git clone https://github.cnanopi_a64_defconfigom/crust-firmware/crust
git clone git://git.denx.de/u-boot.git

#### For compiling Bl31.bin ####
cd arm-trusted-firmware
make CROSS_COMPILE=aarch64-linux-gnu- PLAT=sun50i_a64 DEBUG=1 bl31
### For complimg scp.bin Download the toolchain ###
cd ...
wget https://musl.cc/or1k-linux-musl-cross.tgz
tar xf or1k-linux-musl-cross.tgz
cd crust
make CROSS_COMPILE=..//or1k-linux-musl-cross/bin/or1k-linux-musl- pinephone_defconfig
make CROSS_COMPILE=..//or1k-linux-musl-cross/bin/or1k-linux-musl-
cd ..//u-boot
### For M3X board downlaod patch m3x-uboot.patch #####

