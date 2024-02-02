Acceptance Tests
================

Prior to user operations or after upgrades, the beamline should be able to perform the following tests


Starting bluesky
----------------
◻ Start bluesky. For testing, you may need to set the correct conda environment

    .. code-block:: bash

       $ bsui
       $ BS_ENV=2024-1.0-py310-tiled bsui


General Functions
-----------------
◻ Change energy ::

    [1] %mov energy 12
    [2] energy.mov(12)

◻ Optimize the beam ::

    [3] RE(peakup())

◻ Set an ROI on the detector ::

    [4] setroi(1, "Fe")

◻ Clear the ROIs on the detector ::

    [5] clearroi()

Spectroscopy
------------
◻ Get the binding/absorption energy of an element ::

    [6] getbindingE("Fe")
    [7] getbindingE("Au", "l3")

◻ Get the emission energy of an element ::

    [8] getemissionE("Fe")
    [9] getemissionE("Au", "la1")

◻ Run a XANES plan ::

    [10] Fe_K = getbindingE("Fe")
    [11] RE(xanes_plan([Fe_K-100, Fe_K-20, Fe_K+50, Fe_K+150],
                       [2, 1, 2],
                       acqtime=1,
                       filename="FeTest"))

Imaging
-------
◻ Fly-scan Imaging ::

    [12] RE(nano_scan_and_fly(-5, 5, 21, 0, 5, 11, 0.050))  # May need to change coordinates
    [13] RE(nano_y_scan_and_fly(-5, 5, 21, 0, 5, 11, 0.050))
    [14] RE(coarse_scan_and_fly(-25, 25, 51, -5, 5, 11, 0.250))
    [15] RE(coarse_y_scan_and_fly(-25, 25, 51, -5, 5, 11, 0.250))

◻ Step-scan Imaging. Note that this function uses step size instead of number of points ::

    [16] RE(nano_xrf(-5, 5, 1, -1, 1, 1, snake=True))
    [17] RE(nano_xrf(-5, 5, 1, -1, 1, 1, snake=False))

Troubleshooting
---------------
| ◻ Try using ``CTRL-C`` to pause and resume a scan
| ◻ Try tripping one of the suspenders, such as one of the photon shutters, to see if the scan will automatically pause and resume

Data analysis
-------------
| ◻ XANES data automatically exports to the user folder
| ◻ Athena starts using ``dathena``
| ◻ Athena can access and open the collected XANES data
| ◻ ``run-pyxrftools`` will load and can access scan data
| ◻ Imaging data is automatically exported, or can be made using ``make_hdf``
| ◻ PyXRF starts using ``run-pyxrf``
| ◻ PyXRF can load the imaging data and save the data to the file
