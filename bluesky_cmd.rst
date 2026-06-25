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
XRF Map - *Perform a high-resolution, position-based fly scan. Return an image with dimensions (numX, numY)*

.. code-block::

   Bluesky@SRX [1] RE(xrf_map(startX, stopX, numX,
                              startY, stopY, numY, dwell))

.. function:: xrf_map(startX, stopX, numX, startY, stopY, numY, dwell, fly_on_y=False, resolution="nano")

   Collect an XRF map given the specified range that starts at (startX, startY) and ends at (stopX, stopY) with a shape of (numX, numY).

   :param startX: starting X position
   :param stopX: stopping X position
   :param numX: number of points to collect in X
   :param startY: starting Y position
   :param stopY: stopping Y position
   :param numY: number of points to collect in Y
   :param dwell: desired time per point
   :param fly_on_y: fly in the Y direction, defaults to False
   :type fly_on_y: bool, optional
   :param resolution: set to "coarse" for larger maps. Be sure to use the coarse motor coordinates, defaults to "nano"
   :type resolution: str, optional

   .. warning::
      As of June 30, 2026, the following functions have been deprecated in favor of :func:`xrf_map`. Please update your scripts to use :func:`xrf_map`. ::
   
         Bluesky@SRX [1] RE(nano_scan_and_fly(startX, stopX, numX,
                                              startY, stopY, numY, dwell))
         Bluesky@SRX [2] RE(nano_y_scan_and_fly(startY, stopY, numY,
                                                startX, stopX, numX, dwell))
         Bluesky@SRX [3] RE(coarse_scan_and_fly(startX, stopX, numX,
                                                startY, stopY, numY, dwell))
         Bluesky@SRX [4] RE(coarse_y_scan_and_fly(startY, stopY, numY,
                                                  startX, stopX, numX, dwell))

Step scan - *Perform a step scan. Note: these arguments take a step size, not the number of points.* ::

    Bluesky@SRX [1] RE(nano_xrf(startX, stopX, stepX,
                                startY, stopY, stepY, dwell))

XAS Spectroscopy
****************
Print element binding energies - *Print the binding energies for the element of interest. The "best" edge in eV is returned as available.* ::

    Bluesky@SRX [1] Fe_k = getbindingE('Fe')

Print element emission energies - *Print the emission energies for the element of interest.* ::

    Bluesky@SRX [1] getemissionE('Fe')

XANES scan - *Run a XANES scan. This scan has 3 regions with different steps spanning the iron K-edge.* ::

    Bluesky@SRX [1] RE(xanes_plan(erange=[Fe_k-50, Fe_k-10, Fe_k+50, Fe_k+150],
                                  estep=[2.0, 1.0, 2.0],
                                  acqtime=1.0,
                                  samplename='Fe foil'))

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
