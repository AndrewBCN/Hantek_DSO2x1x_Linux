The Pre-Built folder contains the already built u-boot, Linux kernel, dtb file and root filesystem to run Linux on a Hantek DSO2x1x.

Using the sunxi-fel utility, we can load the four files through the USB cable and boot Linux with a serial console on the same USB cable using the following command:

sudo sunxi-fel -p -v uboot ./output/images/u-boot-sunxi-with-spl.bin write 0x80008000 ./output/images/zImage write 0x80700000 ./output/images/devicetree.dtb write 0x80800000 ./output/images/rootfs.cpio.uboot

(obviously the paths to the files need to be adjusted)

This will download the files to the DSO showing a progress bar, and then transfer control to u-boot, which will start the Linux kernel at the specified address. The kernel then finds the compressed root filesystem, decompresses it and runs init.

At this stage you will find a new ACM (serial) device has been created on the host, and one can start a console using for example the screen program:

sudo screen /dev/ttyACM0

Pressing <Enter> will display the login prompt, the user is root and the password is nano.

