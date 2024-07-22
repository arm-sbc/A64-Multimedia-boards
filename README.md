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

### Compiling
