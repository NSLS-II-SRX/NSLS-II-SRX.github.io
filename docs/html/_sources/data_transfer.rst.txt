Data Management
===============
Tools are available to securely transfer data between NSLS-II servers and your home institute. Options include ssh, sftp, and `Globus <Transfer over Globus_>`_.

Useful Links
************
 - `Globus Connect Personal <https://www.globus.org/globus-connect-personal>`_
 - `Globus Tranfer Files Tutorial <https://docs.globus.org/guides/tutorials/manage-files/transfer-files/>`_


Proposal Directories
********************
Each proposal will have its own folder where files are saved and processed. The folders for the proposals at the SRX beamline are found at ``/nsls2/data/srx/proposals``. From there, the proposals are broken down into operating cycles, *e.g.* ``2025-1``. Finally, the prefix ``pass-`` with the proposal number is used to identify each proposal to make the folder name, *e.g.* ``pass-1234``.

Inside each proposal folder, files will be written automatically. During data collection, raw detector data is written and stored in the ``assets/`` folder. This folder is set as read-only. You are welcome to copy this data, but it will be difficult to correlate raw detector files to particular scans.

Additionally, at the completion of each scan, a process will automatically kick-off to export the scan data. If the scan was an XRF map, files will be generated and written to the root proposal directory with the filename ``autorun_scan2D_{scanid}_xs_sumch.h5``. Spectroscopy files will also be written to the root of this proposal directory with a filename of ``scan_{scanid}_xanes.txt``. Finally, a running logfile records the scan ID, UID, and some scan parameters for each scan that is run.


Transfer over Globus
********************
Globus is an efficient system for transferring large data sets and folders. The Globus endpoint for NSLS-II systems is found at `globus.nsls2.bnl.gov <https://globus.nsls2.bnl.gov>`_. The Globus origin ID is ``819379a8-47db-439d-a5ba-a2387b79add9``

Setup Globus Connect Personal
`````````````````````````````
#. Download and install Globus Connect Personal
#. Run the application. If this is the first time, it should run a setup.
#. Click to Login. This should bring up a website. Choose "Brookhaven National Laboratory" as the organization. Click Continue.
#. Login to the BNL Single Sign On using your BNL account.
#. Provide a label for this Endpoint and click Allow. 
#. Provide a collection name and description. Now you have an endpoint to transfer data to locally.
#. Make sure to leave the Globus Personal Connect running.

Locate Proposal Data
````````````````````
#. Go to the NSLS-II Globus endpoint. Make usre the organization login is set to "Brookhaven National Laboratory". Click on Continue and login to the BNL Single Sign On using your BNL account and password.
#. Once logged on, the Globus main page should appear. The collection at the top should say "NSLS2"
#. If there is a message saying that "Authentication/Consent is required for Globus transfer service to manage data in this collection", click Continue. Click on your email address. Allow Globus Web App to manage data using Globus Transfer.
#. Once logged in, you may start off in your home directory, ``/nsls2/users/your_user_name``
#. In the Path textbox, the location of the proposals can be entered. It is convenient to start at ``/nsls2/data/srx/proposals/``. From there the cycle, *e.g.* ``2025-1``, is selected followed by the folder that corresponds with the proposal number, *e.g.* ``pass-{proposal number}``.
#. At this point, the contents of the proposal directory are displayed. Data can be downloaded or transfered from here.
#. Select your files for download. We recommend ommitting the ``assets/`` folder. Click on Transfer of Sync to... Another panel will pop up where you can select your local Enpoint. Choose a location to download the data. Click start to start the transfer.