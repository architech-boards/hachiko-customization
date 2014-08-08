U-boot
======

The bootloader used by @board@ board is **U-Boot**. If you need to modify the bootloader or
to recompile it you have two ways to get the sources:

* use the sources you find in Yocto build directory after having compiled at least once a yocto image, or
* download the official u-boot release, than patch it with the BSP patches for @board@ board.

Anyway, we will assume in this guide that u-boot sources will be copied to:

.. host::

 | /home/@user@/Documents/u-boot

and such directory does not yet exists on your PC.
Of course, you are free to choose the path you like the most for u-boot sources, just remember
to replace the path used in this guide with your custom path.

From Yocto sources
------------------

The first way is based on the sources set up by the Yocto build system. However, it is never
advisable to work with the sources in the Yocto build directory, if you really want to modify
the source code inside the Yocto environment we strongly suggest to refer to the official Yocto
documentation. To avoid messing up Yocto recipes and installation, it is desirable to copy the
patched u-boot sources you find in the build directory elsewhere. The directory we are talking
about is this one:

.. host::

 | /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/work/@machine-name@-poky-linux-@eabi@/u-boot/2013.04-r0/u-boot-2013.04/

Replace:

.. host::

 | /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/

all over this chapter with your custom build directory path if you are not working with the default SDK 
build directory.

From the official u-boot release
--------------------------------

The second way is to get the official U-Boot sources and patch them with @board@ BSP patches.
@board@ board uses U-Boot version 2013.04, which can be downloaded from:

`ftp://ftp.denx.de/pub/u-boot/u-boot-2013.04.tar.bz2 <ftp://ftp.denx.de/pub/u-boot/u-boot-2013.04.tar.bz2>`_.

with this command:

.. host::

 | cd /home/@user@/Documents
 | wget ftp://ftp.denx.de/pub/u-boot/u-boot-2013.04.tar.bz2

then extract the tarball:

.. host::

 | tar -xjf u-boot-2013.04.tar.bz2
 | mv u-boot-2013.04 u-boot

Patches are to be found in the Yocto meta-layer **@meta-layer@**. You can use them right away if you are
working with the SDK:

.. host::

 | patch -p1 -d /home/@user@/Documents/u-boot < /home/@user@/architech_sdk/architech/@board-alias@/yocto/@meta-layer@/recipes-bsp/u-boot/files/0001-Add-bps-patch-v2.0.0.patch
 | patch -p1 -d /home/@user@/Documents/u-boot < /home/@user@/architech_sdk/architech/@board-alias@/yocto/@meta-layer@/recipes-bsp/u-boot/files/0002-Add-hachiko-support.patch

However, if you are not working with the official SDK the most general solution to check them out and patch
the sources is:

.. host::

 | cd /home/@user@/Documents
 | git clone -b dora https://github.com/architech-boards/@meta-layer@.git 
 | patch -p1 -d /home/@user@/Documents/u-boot < /home/@user@/Documents/@meta-layer@/recipes-bsp/u-boot/files/0001-Add-bps-patch-v2.0.0.patch
 | patch -p1 -d /home/@user@/Documents/u-boot < /home/@user@/Documents/@meta-layer@/recipes-bsp/u-boot/files/0002-Add-hachiko-support.patch

Configuration and board files for @board@ board are in:

.. host::

 | /home/@user@/Documents/u-boot/board/renesas/hachiko/*
 | /home/@user@/Documents/u-boot/include/configs/hachiko.h

Suppose you modified something and you wanted to recompile the sources to test your patches, well, you
need a cross-toolchain (see :ref:`manual_compilation_label` Section). Luckily, the SDK already contains
the proper cross-toolchain. To use it to compile the bootloader or the operating system kernel, just run:

.. host::

 | source /home/@user@/architech_sdk/architech/@board-alias@/toolchain/environment-nofs

then you can run these commands to compile it:

.. host::

 | cd /home/@user@/Documents/u-boot/
 | make mrproper
 | make @machine-name@
 | make


Once the build process completes, you can find *u-boot.bin* file inside directory */home/@user@/Documents/u-boot*.

If you are not working with the virtual machine, you need to get the toolchain from somewhere.
The most comfortable way to get the toolchain is to ask *Bitbake* for it:

.. host::

 | cd /path/to/yocto/directory
 | source poky/oe-init-build-env
 | bitbake meta-toolchain

When *Bitbake* finishes, you find an installer script under directory:

.. host::

 | /path/to/yocto/directory/build/tmp/deploy/sdk/

Run the script and you get, under the installation directory, a script to *source* to get your environment
almost in place for compiling. The name of the script is:

.. host::

 | environment-setup-cortexa9hf-vfp-neon-poky-linux-@eabi@

Anyway, the environment is not quite right for compiling the bootloader and the Linux kernel, you need to unset
a few variables first to get it ready:

.. host::

 | unset CFLAGS CPPFLAGS CXXFLAGS LDFLAGS

Here you go, you now have the proper working environment to compile *u-boot* (or the Linux kernel).

