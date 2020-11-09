# Nuvoton NUC980 Development Board Bootable Linux Image (Buildroot)

This repository contains a Buildroot config extension. That means fully building the U-Boot image, Linux kernel, the rootfs image and the final partitioned binary image for flashing onto the bootable SD card.

There was reasonable effort to keep config files readable, e.g. here is the main Buildroot defconfig file: [configs/nuc980_devboard_defconfig](configs/nuc980_devboard_defconfig).

## Building the Image

download Buildroot and extract it into a folder.

Before building, install these Ubuntu packages:

```sh
sudo apt install swig python-dev fakeroot devscripts
```

If there are still error messages during later build, try installing these (sorry, did not clean up the list yet, some might be unnecessary):

```sh
sudo apt install -y chrpath gawk texinfo libsdl1.2-dev whiptail diffstat cpio libssl-dev
```

Then, create initial build configuration:

```sh
BR2_EXTERNAL=<path_to_this_repo> make nuc980_devboard_defconfig
```

Customize Buildroot configuration if needed:

```sh
make menuconfig
```

Proceed with the build:

```sh
make
```

The build may take 1.5 hours on a decent machine, or longer. 

A successful build will produce a `output/images` folder. That folder contains all essential images (uImage, rootfs.tar.gz, u-boot.bin) that can now be written to the bootable SD card.
