# Hantek_DSO2x1x_Linux
![myimage-alt-tag](https://github.com/AndrewBCN/Hantek_DSO2x1x_Linux/blob/main/Pictures/hanteklinuxinside1a_small.jpg?raw=true)
## Linux for the Hantek DSO2000 series using Buildroot

This project provides the files and documentation to build and run from RAM a small Linux distribution for the Hantek DSO2000 series (DSO2C10, DSO2C15, DSO2D10, DSO2D15) "value" DSOs.  
These inexpensive DSOs are powered by an Allwinner F1C200s SOC with 64MB of RAM, and Buildroot can be configured to build u-boot, the Linux kernel, the DTB file and a small root filesystem. Note the Lichee Pi Nano development board uses the F1C100s version of this SOC, with only 32MB of RAM.  
The files output by Buildroot can be uploaded directly to the DSO RAM using sunxi-fel/USB through the USB OTG connector on the back of the DSO, and then Linux can be started configured so that the same USB OTG interface will provide a serial terminal connection and USB mass storage emulation.

In other words: there is absolutely no need to open the scope and this process does not void the warranty, since the NAND flash inside the DSO remains untouched. And the risk of "bricking" the DSO is zero.

This project borrows many ideas and some code from three distinct GitHub repositories and Buildroot projects for the same Allwinner F1C200s SOC:

1. Businesscard Linux by George Hilliard https://github.com/thirtythreeforty/businesscard-linux

2. Embedded Linux for the Lichee Pi Nano by Nick Matantsev https://github.com/unframework/licheepi-nano-buildroot

3. builroot-tiny200 by AODZIP https://github.com/aodzip/buildroot-tiny200

This project is a result of a thread on EEVblog forum about hacking these Hantek DSOs:

https://www.eevblog.com/forum/testgear/hacking-the-dso2x1x/

## Pre-built files

The Pre-Built folder contains the files required to boot Linux on a DSO2x1x, so the instructions for building below can be skipped.

## Building

We use Buildroot (www.buildroot.org) to build all the required packages to boot Linux on the Hantek DSO2x1x. The building process takes a couple of hours or more depending on the speed of your machine and Internet connection.

1. Git clone this project and cd into the directory just created.
2. Download the Buildroot tarball (buildroot-2021.05.tar.gz) and extract it into this project directory. The recommended version is the one we tested: buildroot-2021.05. This will create a directory /buildroot-2021.05 and you should cd into it.
3. Edit the .gitignore file; it should contain a single line with the character "\*" in it.
4. Prepare the buildroot configuration file: make BR2_EXTERNAL=$PWD/../ hantek_dso2k_defconfig
5. [optional] At this point you can if you want edit the default Buildroot configuration file and save your own version. Check the Buildroot manual for instructions.
6. Start the build: make. You can make yourself a cup of tea and/or watch a movie, because the build process takes a couple of hours or more. There may be warnings and even errors during the build process, due to version mismatches between the gcc version installed on your machine and the original version used by developers of various packages, but these are usually trivial. See BR2ERRORS.txt for details.

## Loading Linux using sunxi-fel/USB

Refer to this page for details: https://linux-sunxi.org/FEL/USBBoot  

### From a PC running Windows

### From a PC running Linux

## Opening a root shell and transferring files to/from the DSO2x1x
If Linux correctly booted on the Hantek DSO (it take just a few seconds), then two USB devices will be detected on your Windows or Linux PC connected to the DSO:
1. A serial port running at 115200 baud rate, with a root shell, where you should login as root (there is no password). If you are using Linux the serial device will show up as /dev/ttyACM0 or /dev/ttyACM1. You can open a terminal using screen or minicom.
2. A small USB storage device with a FAT partition and the file README.txt. This is a tiny r/w space which you can use to exchange files directly between your PC and the DSO. Note that the files in this virtual USB drive will be lost once the DSO is turned off.

## Developers

If you want to change the u-boot or Linux kernel version, or help development for this project, or simply "do it your own way" you can examine the default Buildroot configuration file and modify it as explained above. Same applies to other configuration files, as well as all the other files in this project: once you think you have found/solved a bug or added a feature that you would like included here, just open an issue or a pull request.

## Contributors

Main contributor: AndrewBCN.<br/>
DSO2x1x master hacker and tester: DavidAlfa.<br/>
DSO2x1x and Lichee Pi Nano tester: aika.<br/>
