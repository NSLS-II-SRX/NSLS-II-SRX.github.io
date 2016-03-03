Pixirad detector
================

IOC
---

+-------------------------------+-------------------+
| Item                          | Value             |
+===============================+===================+
| Host name                     | xf05idd-ioc-det03 |
+-------------------------------+-------------------+
| IOC process name              | det03             |
+-------------------------------+-------------------+
| Detector interface IP address | 192.168.0.2       |
+-------------------------------+-------------------+

Boot notes
~~~~~~~~~~

The BIOS is currently set to network boot before local hard drive boot. To
interrupt this, press ESC while the circle spinning next the DHCP is on the
screen. This will interrupt the network boot and progress to the local boot. If
the screen with PXE Boot comes up, restart the computer and press ESC earlier.

eth0 did not come up with an IPv4 address on initial attempts at connecting to
the detector. This was solved by issuing the following commands:

::

  $ sudo ifdown eth0
  $ sudo ifup eth0

For some reason, the above works while ``$ sudo ifconfig eth0 down|up`` did not
work.



