# A64-Multimedia-boards
## General Instructions
The uboot and kernel device tree files are available for download , either as a patch or as individual files.
for compiling , follow below instructions.

TESTED on Ubuntu 22.04

```sh
apt-get install gcc-arm-linux-gnueabihf gcc-aarch64-linux-gnu flex bison swig python3-dev device-tree-compiler git libncurses-dev python3-setuptools libssl-dev pip2 pip
pip install pyelftools

git clone https://github.com/arm-sbc/A64-Multimedia-boards.git
git clone https://github.com/ARM-software/arm-trusted-firmware.git
git clone https://github.cnanopi_a64_defconfigom/crust-firmware/crust
git clone git://git.denx.de/u-boot.git

####for U-boot it required arm trusted firmware and scp ( scp is optional, the board will boot without scp) ####
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
cd ..
patch -Np1 -i m3x-uboot.patch
export BL31=..//arm-trusted-firmware/build/sun50i_a64/release/bl31.bin
export SCP=..//crust/build/scp/scp.bin
make CROSS_COMPILE=aarch64-linux-gnu- a64-arm-sbc-m3x_defconfig
make CROSS_COMPILE=aarch64-linux-gnu-


