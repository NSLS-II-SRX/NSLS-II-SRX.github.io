Beamline Staff Pages
====================

The information provided on this page is directed towards helping beamline staff.


Quick Links
-----------
#. `Analog camera web server <http://10.5.0.33>`_
#. `Trac ticket system <https://controlsweb.nsls2.bnl.gov/trac/>`_
#. `SRX Posted SAFs <https://nsls2bid.bnl.gov/SAF/Index/5-ID>`_
#. `SRX Olog <http://xf05id-ca1.cs.nsls2.local/logbook/index.html>`_
#. `SRX IOCs and Motor Controllers <To Do>`_
#. `SRX Radiation Safety Component Checklist <https://ps.bnl.gov/docs/Reference/NSLS-II%20Beamline%205-ID%20Radiation%20Safety%20Component%20Checklist%20TEMPLATE.pdf>`_
#. `NSLS-II Controls Documentation <http://nsls-ii.github.io/>`_
#. `NSLS-II IP Address Management <https://controlsweb01.nsls2.bnl.gov/IP/?page=login&section=timeout>`_
#. `NSLS-II Sharepoint Documentation <https://ps.bnl.gov/phot/ros/Shared%20Documents/MAXIMO%20Development/Beamlines/LT-R-XFD-CO-DR-SRX-002_Rev1.xlsx>`_


Setting up Users
----------------
#. Post SAF to `PASS <http://passadmin.bnl.gov>`_
#. Update user-specific metadata
    * Open /home/xf05id1/ipython_ophyd/90-userdata.py
    * Update proposal dictionary with information from posted SAF. Save.
    * Restart bluesky.
#. Perform beamline specific training. `5-ID BST form <https://www.bnl.gov/ps/training/Beamline-BST-Forms/PS-BST-5-ID.pdf>`_


Beamline Setup
--------------

