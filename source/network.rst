Network
=======

The network PHY is provided by Renesas's chip 60610 (*U6*).
Within Linux, you can see the network interface as **eth0**.

If you want that configuration to be brought up at boot you can add a few line in file */etc/network/interfaces*, for
example, if you want *eth0* to have a fixed ip address (say 192.168.0.10) and MAC address of value 1e:ed:19:27:1a:b6
you could add the following lines:

.. board::

 | auto eth0                                       
 | iface eth0 inet static                          
 |     address 192.168.0.10
 |     netmask 255.255.255.0
 |     hwaddress ether 1e:ed:19:27:1a:b6      

