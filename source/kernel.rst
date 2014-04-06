Linux Kernel
============

As seen for **U-Boot** in the previous section, the first step is to get the kernel
sources, which in this guide we assume that they will be copied to directory:

.. host::

 /home/@user@/Documents/kernel

You are free to choose the path you like the most for the kernel sources, just remember
to replace the path used in this guide with your custom path.
The suggested way, even for the kernel, to get the sources is to take them from the Yocto
build directory (copying them in the aforementioned directory to avoid messing up Yocto):

.. host::

 /home/@user@/architech_sdk/architech/@board-alias@/yocto/build/tmp/work/@machine-name@-poky-linux-@eabi@/linux/3.8.13-r2/linux-3.8.13/

or from the vanilla kernel tarball at this URL:

 `https://www.kernel.org/pub/linux/kernel/v3.0/patch-3.8.13.bz2 <https://www.kernel.org/pub/linux/kernel/v3.0/patch-3.8.13.bz2>`_.

and patch it using the patches found in @board@ BSP meta-layer:

.. host::

 patch -p1 -d /home/@user@/Documents/kernel < /home/@user@/architech_sdk/architech/@board-alias@/yocto/@meta-layer@/recipes-kernel/linux/files/\*.patch

If you are not developing from within the official SDK, the most general solution to check
them out and patch the sources is:

.. host::

 | cd /home/@user@/Documents
 | git clone -b dora https://github.com/architech-boards/@meta-layer@.git 
 | patch -p1 -d /home/@user@/Documents/kernel < /home/@user@/Documents/@meta-layer@/recipes-kernel/linux/files/\*.patch

To compile the kernel just execute these commands:

.. host::

 | cd /home/@user@/Documents/kernel
 | source /home/@user@/architech_sdk/architech/@board-alias@/toolchain/environment-nofs
 | make @machine-name@_defconfig
 | make uImage dtbs

If you are not developing from within the original SDK, you are going to need to
:ref:`install the cross toolchain <manual_compilation_label>`.
The output of the compilation process is:

.. host::

 /home/@user@/Documents/kernel/arch/arm/boot/uImage
 /home/@user@/Documents/kernel/arch/arm/boot/dts/rza1-hachiko.dtb

