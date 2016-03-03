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
* Weak-link flexure for all stages.
* No overconstrained systems.

Motion control 
^^^^^^^^^^^^^^

Motion axes 
~~~~~~~~~~~

+---------------------------------------+------+-------------+-------------+-----------------------------------+
| Mirror system                         | Axis | Motor type  | Controller  | Notes                             |
+=======================================+======+=============+=============+===================================+
| Mir:2 (high-flux vertical focusing)   | X    | SmarAct (2) | SmarAct MCS | Limited yaw capability            |
+---------------------------------------+------+-------------+-------------+-----------------------------------+
|                                       | Y    | Stepper (4) | Delta Tau   | Overconstrained mechanical system |
+---------------------------------------+------+-------------+-------------+-----------------------------------+
|                                       | Z    | SmarAct (1) | SmarAct MCS |                                   |
+---------------------------------------+------+-------------+-------------+-----------------------------------+
| Mir:3 (high-flux horizontal focusing) | X    | SmarAct (2) | SmarAct MCS | Limited yaw capability            |
+---------------------------------------+------+-------------+-------------+-----------------------------------+
|                                       | Y    | Stepper (1) | Delta Tau   |                                   |
+---------------------------------------+------+-------------+-------------+-----------------------------------+


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
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Mechanics
^^^^^^^^^

* Weak link flexures for all translations
* Downstream X translation motor is in line with mirror center, so this motor
  does not move to implement pitch movement.

Motion control 
^^^^^^^^^^^^^^

* Roll motor has approximately +/- 5 degrees of movement.

Motion axes 
~~~~~~~~~~~

+---------------------------------------------+------+-------------------+-----------------+------------------------+
| Mirror system                               | Axis | Motor type        | Controller      | Notes                  |
+=============================================+======+===================+=================+========================+
| Mir:4 (high-resolution vertical focusing)   | X    | SmarAct (2)       | SmarAct MCS     | Limited yaw capability |
+---------------------------------------------+------+-------------------+-----------------+------------------------+
|                                             | Y    | Stepper (2)       | Delta Tau       |                        |
+---------------------------------------------+------+-------------------+-----------------+------------------------+
|                                             | Z    | SmarAct (1)       | SmarAct MCS     |                        |
+---------------------------------------------+------+-------------------+-----------------+------------------------+
| Mir:5 (high-resolution horizontal focusing) | X    | SmarAct (2)       | SmarAct MCS     | Limited yaw capability |
+---------------------------------------------+------+-------------------+-----------------+------------------------+
|                                             | Y    | Stepper (1)       | Delta Tau       |                        |
+---------------------------------------------+------+-------------------+-----------------+------------------------+
|                                             | Roll | Attocube ECGt5050 | Attocube ECC100 |                        |
+---------------------------------------------+------+-------------------+-----------------+------------------------+


Instructions 
------------

SmarAct motor closed-loop operation 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
* To activate closed-loop operation, set the 'Closed Loop' button on the desired
  axis to Enable.
* Moving the axis will reset this to 'Disable' but the axis will remain in
  closed-loop. 
* The motor should show 'Holding' after the move has complete. 'Stopped'
  indicates open-loop operation.
* To deactivate closed-loop operation, set the 'Closed Loop' button on the
  desired axis to Disable. Even if it is already showing Disable, this will move
  the motor into open-loop operation.
* Pressing 'Stop' will stop movement and put the motor into open-loop.

Mir:5 roll referencing
~~~~~~~~~~~~~~~~~~~~~~
* Turn on both auto-reference and auto-reset in Advanced display.
* Move axis over full range until 'Referenced' light turns green.
* Turn off both auto-reference and auto-reset.




