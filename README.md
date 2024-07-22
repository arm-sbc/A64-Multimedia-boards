# A64-Multimedia-boards
## General Instructions
The uboot,kernel and device tree files are available for download , either as a patch or as individual files.
for compiling , follow below instructions.

TESTED on Ubuntu 22.04

```sh
apt-get install gcc-arm-linux-gnueabihf gcc-aarch64-linux-gnu flex bison swig python3-dev device-tree-compiler git libncurses-dev python3-setuptools libssl-dev pip2 pip picocom
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
cd u-boot
git tag -l
git branch -C XXXXX ( choose teh latest branch) 

patch -Np1 -i m3x-uboot.patch

export BL31=..//arm-trusted-firmware/build/sun50i_a64/release/bl31.bin
export SCP=..//crust/build/scp/scp.bin

make CROSS_COMPILE=aarch64-linux-gnu- a64-arm-sbc-m3x_defconfig
make CROSS_COMPILE=aarch64-linux-gnu-

#### flashing uboot to sd-card,  first clean the sd-card ###
#### use any of below commands based on your requirement ###

sudo dd if=/dev/zero of=/dev/sdX bs=1M count=1  # clear partition and boot sector
sudo dd if=/dev/zero of=/dev/sdX bs=1k count=1023 seek=1 # clear bootloader without partitions
sudo dd if=/dev/zero of=/dev/sdX bs=8192 # to clean it completely

then

sudo dd if=u-boot-sunxi-with-spl.bin of=/dev/sdX bs=1024 seek=8
sync

### now you can insert the card into the board, connect the debug port with a serial cable , only TX, RX and GND port,
do not connect the voltage)
incase of picocom installed and using USB UART cable)

sudo picocom -b 115200 -r -l /dev/ttyUSB0

#### you will see bootlog

#### now remove the sd-card and put back into the computer,
#### create partion of OS ###
sudo fdisk /dev/sdX
type n
### then enter, enter again and again
sudo mkfs.ext4 /dev/sdX1
this will create a ext4 partition.

#### compiling kernel #####
go to https://kernel.org/
then select the stable veriosn nd download the tarballs.
then tar xf linux-6.9.X.tar.xz
cd linux-6.9.X

