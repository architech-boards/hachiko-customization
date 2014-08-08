Meta Layer
==========

A Yocto/OpenEmbedded meta-layer is a directory that contains recipes,
configuration files, patches, and others things all needed by Bitbake to
properly "see" and build a BSP, a distribution, and a (set of) package(s).

meta-hachiko is stored in a git repository that can be cloned with:

.. host::

 | git clone -b dora https://github.com/architech-boards/@meta-layer@.git

For information about Yocto, Bitbake and the directories tree inside the
meta-layer, please refer to the Yocto documentation.

@board@ meta-layer defines two different machines: **hachiko** and **hachiko64**,
the latter to be used when an external SDRAM is available on the board.
Whereas *hachiko64* machine can be used for virtually any distro and image
available on Yocto, *hachiko* machine must use a custom tailored distro and image
to be able to fit in the limited amount of SRAM available on-chip.
This documentation is about **@machine-name@** machine.

To manually select board and distribution for *Bitbake*, make sure that file
*local.conf*, that in the SDK has this path:

.. host::

 | /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/conf/local.conf

contains the assignment of these variables:

.. host::

 | MACHINE = "@machine-name@"
 | DISTRO = "@distro-name@"

When asked to build an image, *Bitbake*/*Hob* produces several files as output, of
which these are needed to build the whole system:

* the Linux kernel - file *uImage*

* the device tree - file *uImage-rza1-hachiko.dtb*

* U-boot bootloader - file *u-boot.bin*

* the root file system - file *\*.tar.bz2* 

Within the SDK, the files will be emitted to directory:

.. host::

 | /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/deploy/images/@machine-name@/

If you are not working with the SDK, just replace:

.. host::

 | /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/

with your build directory path.
