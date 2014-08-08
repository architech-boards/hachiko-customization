To deploy the root file system, you are going to need an USB flash drive.

.. warning::

 The USB flash drive content will be lost forever!

1. Umount the device:

.. host::

 | sudo umount /path/to/your/USB/device/partition

2. Align a new partition to the first sector of your USB device:

.. host::
 
 | sudo sfdisk /path/to/your/USB/device << EOF
 | 0,
 | EOF


3. Format it as an *EXT2* partition:

.. host::

 | sudo mkfs.ext2 /path/to/your/USB/device/partition

4. Extract your image inside such a media:

.. host::

 | sudo tar -xjf /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/deploy/images/@machine-name@/@quickstart-image@-@machine-name@.tar.bz2 -C /path/to/usb/media

5. Copy the kernel to the USB flash drive:

.. host::

 | cp /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/deploy/images/@machine-name@/uImage /path/to/usb/media/boot

6. Now copy the device tree:

.. host::

 | cp /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/deploy/images/@machine-name@/uImage-rza1-hachiko.dtb  /path/to/usb/media/boot/rza1-hachiko.dtb


7. Unmount the flash drive from your system

8. Insert the USB Flash drive in the USB port at the bottom of the USB connector of @board@ board
