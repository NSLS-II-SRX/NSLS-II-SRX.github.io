SRX KB mirrors
==============

Introduction
------------

There are two sets of KB mirrors in the SRX endstation, one high-flux pair and
one high-resolution pair.

High-flux
---------

Mir:2 - High-flux VFM
~~~~~~~~~~~~~~~~~~~~~

Mechanics
^^^^^^^^^

* Weak link flexures for all translations
* Vertical translation system has four stepper motors, so is
  overconstrained. Extra axis is twist, and needs to be maintained at
  zero. 
* Horizontal translation for stripe selection done by two SmarAct actuators.
  These actuators have limited ability to yaw, and as a result can get stuck.
* Longitudinal translation by single SmarAct actuator.


Motion control 
^^^^^^^^^^^^^^
* Delta Tau coordinate system implemented for Mir:2 vertical movements: vertical
  translation, pitch, roll, twist.
* Twist should be maintained at zero.
* A PLC monitors the twist and deactivates the vertical motors if the calculated
  twist exceeds a specified value.

Mir:3 - High-flux HFM
~~~~~~~~~~~~~~~~~~~~~ 

Mechanics
^^^^^^^^^

Motion control 
^^^^^^^^^^^^^^

Motion axes 
~~~~~~~~~~~

High-resolution
---------------

Mir:4 - High-resolution VFM
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mechanics
^^^^^^^^^

* Weak link flexures for all translations
* Vertical translation system has two stepper motors, so is not
  overconstrained. 

Motion control 
^^^^^^^^^^^^^^

Mir:5 - High-resolution HFM
~~~~~~~~~

Mechanics
^^^^^^^^^

Motion control 
^^^^^^^^^^^^^^

Motion axes 
~~~~~~~~~~~


