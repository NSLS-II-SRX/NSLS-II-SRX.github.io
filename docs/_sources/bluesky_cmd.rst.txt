Bluesky Commands
================
Below is a list of useful commands for running the SRX beamline. Previous commands can be seen by hitting the up arrow in Bluesky. To search through them, you can start typing a command before hitting the up arrow to filter your history.

Starting Bluesky
****************
Start Bluesky - *Bluesky can be started by going to the top left corner of the screen and choosing Activities. Then click on the Bluesky icon - a blue cloud with a b - to automatically open a new terminal and start Bluesky.* 

*Alternatively, start Bluesky from an existing terminal.* ::

    $ bsui

After starting Bluesky, it is important to confirm that the proposal number in the terminal matches the experiment.

General Functions
*****************
Change X-ray energy - *Either command can be used below. The energy can be entered in units of eV or keV.* ::

    Bluesky@SRX [1] %mov energy 7.2
    Bluesky@SRX [2] energy.move(7.2)

Optimize the beam - *Maximize the X-ray flux.* ::

    Bluesky@SRX [1] RE(peakup())

Optimize the ion chambers - *Check that the ion chambers have their ideal preamp settings.* ::

    Bluesky@SRX [1] RE(optimize_scalers())

Setting a region of interest - *Set the ROI on the detector. The specific line is optional.* ::

    Bluesky@SRX [1] setroi(1, 'Fe')
    Bluesky@SRX [2] setroi(1, 'Fe', 'ka1')

XRF Imaging
***********
**XRF Fly Scan Map**

.. code-block::

   Bluesky@SRX [1] RE(xrf_map(xstart, xstop, xnum,
                              ystart, ystop, ynum, dwell, sample_name="my special sample"))

.. function:: xrf_map(xstart, xstop, xnum, ystart, ystop, ynum, dwell, sample_name="", fly_on_y=False, resolution="nano", extra_dets=[], vlm_snapshot=True, center=True)

   Collect an XRF map given the specified range that starts at (xstart, ystart) and ends at (xstop, ystop) with a shape of (xnum, ynum).

   :param xstart: starting X position
   :type xstart: float
   :param xstop: stopping X position
   :type xstop: float
   :param xnum: number of points to collect in X
   :type xnum: int
   :param ystart: starting Y position
   :type ystart: float
   :param ystop: stopping Y position
   :type ystop: float
   :param ynum: number of points to collect in Y
   :type ynum: int
   :param dwell: desired time per point
   :type dwell: float
   :param sample_name: a human-readable name for the sample, defaults to an empty string, ""
   :type sample_name: str, optional
   :param fly_on_y: fly in the Y direction, defaults to False
   :type fly_on_y: bool, optional
   :param resolution: set to "coarse" for larger maps. Be sure to use the coarse motor coordinates, defaults to "nano"
   :type resolution: str, optional
   :param extra_dets: add additional detectors - such as *eiger*, *dexela*, or *merlin* - to your maps, defaults to an empty list
   :type extra_dets: list of ophyd objects, optional
   :param vlm_snapshot: collect an optical image at the beginning and end of the scan, defaults to True
   :type vlm_snapshot: bool, optional
   :param center: move the scanner stages to the center at the end of the scan, defaults to True
   :type center: bool, optional

   .. warning::
      As of September 1, 2026, the following functions have been deprecated in favor of :func:`xrf_map`. Please update your scripts to use :func:`xrf_map`. Beamline staff are happy to assist using the new function. ::
   
         Bluesky@SRX [1] RE(nano_scan_and_fly(startX, stopX, numX,
                                              startY, stopY, numY, dwell))
         Bluesky@SRX [2] RE(nano_y_scan_and_fly(startY, stopY, numY,
                                                startX, stopX, numX, dwell))
         Bluesky@SRX [3] RE(coarse_scan_and_fly(startX, stopX, numX,
                                                startY, stopY, numY, dwell))
         Bluesky@SRX [4] RE(coarse_y_scan_and_fly(startY, stopY, numY,
                                                  startX, stopX, numX, dwell))

**XRF Step Scan Map**

.. code-block::

   Bluesky@SRX [1] RE(nano_xrf(xstart, xstop, xnum,
                               ystart, ystop, ynum, dwell, sample_name="my special sample"))

.. function:: nano_xrf(xstart, xstop, xnum, ystart, ystop, ynum, dwell, sample_name="", snake=True)

   Collect an XRF map by stepping through each point. The scan will start at (xstart, ystart) and complete at (xstop, ystop), creating a map with size (xnum, ynum).

   :param xstart: starting X position
   :type xstart: float
   :param xstop: stopping X position
   :type xstop: float
   :param xnum: number of points in X
   :type xnum: float
   :param ystart: starting Y position
   :type ystart: float
   :param ystop: stopping Y position
   :type ystop: float
   :param ynum: number of points in Y
   :type ynum: float
   :param dwell: desired time per point
   :type dwell: float
   :param sample_name: a human-readable name for the sample, defaults to an empty string, ""
   :type sample_name: str, optional
   :param snake: using a snaking scan strategy, defaults to True
   :type snake: bool, optional


XAS Spectroscopy
****************
Print element binding energies - *Print the binding energies for the element of interest. The "best" edge in eV is returned as available.* ::

    Bluesky@SRX [1] Fe_k = getbindingE('Fe')

Print element emission energies - *Print the emission energies for the element of interest.* ::

    Bluesky@SRX [1] getemissionE('Fe')

**XANES scan**

.. code-block::

    Bluesky@SRX [1] RE(xanes_plan(erange=[Fe_k-50, Fe_k-10, Fe_k+50, Fe_k+150],
                                  estep=[2.0, 1.0, 2.0],
                                  dwell=1.0,
                                  sample_name="Fe foil"))

.. function:: xanes_plan(erange, estep, dwell, sample_name="", roinum=1, harmonic=1, vlm_snapshot=True)

   Collect a XANES scan by scanning the incident energy on the sample. The energy points are defined using regions in `erange` with given steps between the points, defined by `estep`.

   :param erange: endpoints for different regions that define the energy points for the scan
   :type erange: list of floats
   :param estep: energy step size for each region
   :type estep: list of floats
   :param dwell: dwell time per energy point
   :type dwell: float
   :param sample_name: a human-readable name for the sample, defaults to an empty string, ""
   :type sample_name: str, optional
   :param roinum: region of interest to measure, default to 1
   :type roinum: int, optional
   :param harmonic: undulator harmonic to use for the scan. The default behavior will use the harmonic with the highest X-ray flux for the current energy. Defaults to 1
   :type harmonic: int, optional
   :param vlm_snapshot: collect an optical image at the beginning and end of the scan, defaults to True
   :type vlm_snapshot: bool, optional

Metadata
********
Print the ``start`` or ``stop`` document for a scan - *A scan ID of 12345 is assumed. A value of -1 can be used to see the previous scan.* ::

    Bluesky@SRX [1] c[12345].start
    Bluesky@SRX [2] c[12345].stop

Print the ``baseline`` information for a scan - *baseline will collect the motor positions at the start (column 1) and completion (column 2) of a scan. There are many motors positions captured so it is helpful to filter the list of values. A scan ID of 12345 is assumed.* ::

    Bluesky@SRX [3] print_baseline(12345)
    Bluesky@SRX [4] print_baseline(12345, key_filter="nano_stage")


Troubleshooting
***************
Pause a scan - *The scan will pause at the next checkpoint.* ::

    CTRL+C

Urgently stop a scan - *With each CTRL-C, Bluesky raises the urgency of stopping the scan.* ::

    CTRL+C x20

Resume a scan - *A scan can be resumed after pausing.* ::

    Bluesky@SRX [1] RE.resume()

Stop a scan - *Stop a scan and label the scan as a success or failure.* ::

    Bluesky@SRX [1] RE.stop()   # Label scan as success
    Bluesky@SRX [2] RE.abort()  # Label scan as failure
