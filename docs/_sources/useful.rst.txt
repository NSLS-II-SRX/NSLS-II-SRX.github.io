Useful Commands
===============
Below is a list of useful commands for running the SRX beamline. Previous commands can be seen by hitting the up arrow in Bluesky. To search through them, you can start typing a command before hitting the up arrow to filter your history.

Starting Bluesky
****************
Start Bluesky - *Start Bluesky from the terminal.* ::

    $ bsui

General Functions
*****************
Change X-ray energy - *Either command can be used below. The energy can be entered in units of eV or keV.* ::

    Bluesky@SRX [1] %mov energy 7.2
    Bluesky@SRX [2] energy.move(7.2)

Optimize the beam - *Maximize the X-ray flux.* ::

    RE(peakup())

Setting a region of interest - *Set the ROI on the detector. The specific edge is optional.* ::

    Bluesky@SRX [1] setroi(1, 'Fe')
    Bluesky@SRX [2] setroi(1, 'Fe', 'ka1')

XRF Imaging
***********
Fly scan - *Perform a high-resolution, position-based fly scan. Return an image with dimensions (numX, numY)* ::

    Bluesky@SRX [1] RE(nano_scan_and_fly(startX, stopX, numX,
                                         startY, stopY, numY, dwell))
    Bluesky@SRX [2] RE(nano_y_scan_and_fly(startY, stopY, numY,
                                           startX, stopX, numX, dwell))

Fly scan - *Perform a coarse, time-based fly scan. Return an image with dimensions (numX, numY)* ::

    Bluesky@SRX [1] RE(coarse_scan_and_fly(startX, stopX, numX,
                                           startY, stopY, numY, dwell))
    Bluesky@SRX [2] RE(coarse_y_scan_and_fly(startY, stopY, numY,
                                             startX, stopX, numX, dwell))

Step scan - *Perform a step scan. Note: these arguments take a step size, not the number of points.* ::

    Bluesky@SRX [1] RE(nano_xrf(startX, stopX, stepX,
                                startY, stopY, stepY, dwell))

XAS Spectroscopy
****************
Print element binding energies - *Print the binding energies for the element of interest. The "best" edge can be returned as available.* ::

    Bluesky@SRX [1] Fe_k = getbindingE('Fe')

Print element emission energies - *Print the emission energies for the element of interest.* ::

    Bluesky@SRX [1] getemissionE('Fe')

XANES scan - *Run a XANES scan. This scan has 3 regions with different steps spanning the iron K-edge.* ::

    Bluesky@SRX [1] RE(xanes_plan(erange=[Fe_k-50, Fe_k-10, Fe_k+50, Fe_k+150],
                                  estep=[2.0, 1.0, 2.0],
                                  acqtime=1.0,
                                  samplename='Fe foil',
                                  filename='Fe_foil']))

Metadata
********
Print the ``start`` or ``stop`` document for a scan - *A scan ID of 12345 is assumed. A value of -1 can be used to see the previous scan.* ::

    Bluesky@SRX [1] db[12345].start
    Bluesky@SRX [2] db[12345].stop

Print the ``baseline`` information for a scan - *baseline will collect the motor positions at the start (column 1) and completion (column 2) of a scan. There are many motors positions captured so it is helpful to filter the list of values. A scan ID of 12345 is assumed.* ::

    Bluesky@SRX [3] print_baseline(12345)
    Bluesky@SRX [4] print_baseline(12345, key_filter="nano_stage")


Troubleshooting
***************
Pause a scan - *The scan will pause at the next checkpoint.* ::

    CTRL+C

Urgently stop a scan - *With each CTRL-C, Bluesky raisens the urgency of stopping the scan.* ::

    CTRL+C x20

Resume a scan - *A scan can be resumed after pausing.* ::

    Bluesky@SRX [1] RE.resume()

Stop a scan - *Stop a scan and label the scan as a success or failure.* ::

    Bluesky@SRX [1] RE.stop()   # Label scan as success
    Bluesky@SRX [2] RE.abort()  # Label scan as failure
