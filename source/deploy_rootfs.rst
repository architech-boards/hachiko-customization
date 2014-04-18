To deploy the root file system, you are going to need an USB flash drive.

.. warning::

 The USB flash drive content will be lost forever!

1. Align a new partition to the first sector of your USB device:

.. host::
 
 | sfdisk /path/to/your/USB/device << EOF
 | 0,
 | EOF


2. Format it as an *EXT2* partition:

.. host::

 | mkfs.ext2 /path/to/your/USB/device/partition

3. Extract your image inside such a media:

.. host::

 | sudo tar -xjf /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/deploy/images/@machine-name@/@quickstart-image@-@board-alias@.tar.bz2 -C /path/to/usb/media

4. Copy the kernel to the USB flash drive:

.. host::

 | cp /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/deploy/images/@machine-name@/uImage /path/to/usb/media/boot

5. Now copy the device tree:

.. host::

 | cp /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/deploy/images/@machine-name@/uImage-rza1-hachiko.dtb  /path/to/usb/media/boot/rza1-hachiko.dtb


6. Unmount the flash drive from your system

7. Insert the USB Flash drive in the USB port at the bottom of the USB connector of @board@ board
