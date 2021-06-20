# Hantek_DSO2x1x_Linux
![myimage-alt-tag](https://github.com/AndrewBCN/Hantek_DSO2x1x_Linux/blob/main/Pictures/hanteklinuxinside1a_small.jpg?raw=true)
## Linux for the Hantek DSO2000 series using Buildroot

This project provides the files and documentation to build and run from RAM a small Linux distribution for the Hantek DSO2000 series (DSO2C10, DSO2C15, DSO2D10, DSO2D15) "value" DSOs.
These inexpensive DSOs are powered by an AllWinner F1C200s SOC with 64MB of RAM, and Buildroot can be configured to build u-boot, the Linux kernel, the DTB file and a small root filesystem.
The files output by Buildroot can then be uploaded directly to the DSO RAM using sunxi-fel/USB, and then Linux can be started which will provide a serial terminal connection and USB mass storage emulation through the USB OTG connector on the back of the DSO.

In other words: there is absolutely no need to open the scope and this process does not void the warranty, since the NAND flash inside the DSO remains untouched.

This project borrows many ideas and some code from three distinct GitHuB repositories and Buildroot projects for the same F1C200s SOC:

1. Businesscard Linux by George Hilliard https://github.com/thirtythreeforty/businesscard-linux

2. Embedded Linux for the Lichee Pi Nano by Nick Matantsev https://github.com/unframework/licheepi-nano-buildroot

3. builroot-tiny200 by AODZIP https://github.com/aodzip/buildroot-tiny200

This project is a result of a thread on EEVBlog forum about hacking these Hantek DSOs:

https://www.eevblog.com/forum/testgear/hacking-the-dso2x1x/

## Pre-built files

The Pre-Built folder contains the files required to boot Linux on a DSO2x1x, so the instructions for building below can be skipped.

## Building

We use Buildroot (www.buildroot.org) to build all the required packages to boot Linux on the Hantek DSO2x1x. The building process takes a couple of hours or more depending on the speed of your machine and Internet connection.

## Loading Linux using sunxi-fel/USB

### From a PC running Windows

### From a PC running Linux

## Opening a root shell and transferring files to/from the DSO2x1x
