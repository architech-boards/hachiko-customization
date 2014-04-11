Root FS
=======

By default, @board@ Yocto/OpenEmbedded SDK will generate two different types of files when you build an image:

* *\*.tar.bz2*, and

* *\*.jffs2*

The *.tar.bz2* file can be expanded in your final medium partition (flash memory or USB stick) or on your host development system and used for build purposes with the Yocto Project.
File *.jffs2* can be written out "as is" on the final medium (usually flash NOR partition) with, for example, *dd* program:

.. host::

 | sudo dd if=/path/to/image.jffs2 of=/path/to/your/USB/device

or 

.. board::

 | flashcp -v /path/to/image.jffs2 /dev/mtd4

.. important::

 Be very careful when you use *dd* or *flashcp* to write to a device to pick up the right device

