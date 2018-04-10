# Team Help Desk

This is a collection of some selected Q&A between the TA/professor and students, which requires rather longer explanation. This is made also for archiving purpose.



## Team Comet

*This team will investigate the magnitude, radial profile, and polarimetric property of the comet if possible.*

### What are the recommended comets to observe or how do we find comets?

*by. Hojun Lee (2018-04-10 20:20 KST)*

I can immediately come up with 2 approaches to find observable comets. First, simple and interactive, manual way. Second, a complicated, automatized way (which I haven't tried by myself).

**Way 1**

1. Google something like "observable comets". You may find some web like [Sky & Telescopes](http://www.skyandtelescope.com/observing/bright-comet-prospects-for-2018/).

2. Go to [JPL/HORIZONS](https://ssd.jpl.nasa.gov/horizons.cgi#results) web-interface. Set

   | Parameter          | Value                                                        |
   | ------------------ | ------------------------------------------------------------ |
   | Ephemeris Type:    | OBSERVER                                                     |
   | Target Body:       | **Comet C/2016 R2 (PANSTARRS)**                              |
   | Observer Location: | **Seoul** **S. Korea** ( 127°03'00.0''E, 37°34'59.9''N )     |
   | Time Span:         | Start=**2018-04-10**, Stop=**2018-06-01**, Step=**1** **h**  |
   | Table Settings:    | QUANTITIES=**1-4,8-10,19,20,23,24,27,33**; elevation cutoff=**30**; skip daylight=**YES** |
   | Display/Output:    | *default* (formatted HTML)                                   |

   * How to set
     * **Ephemeris type**: Click ``change``,  select ``Observer Table``
     * **Target Body**: Click ``change``, enter comet name, e.g., ``C/2016 R2``. For some comets, you will need to select some options --> select the default or the most recent one.
     * **Observer Location**: Click ``change``, enter ``Seoul``.
     * **Time Span**: Click ``change``, leave the start time as is, set stop time to be ``2016-06-01``. I guess you should finish observation by May (to be able to reduce the data within this semester).
     * **Table Settings**: Click ``change``, select ``small-bodies`` button. Go down and set ``elevation cutoff : 30 (deg)``, and check ``skip daylight``. Click ``Use Selected Settings``.

3. Then click ``Generate Ephemerides``.

4. First box (``Object Data Page``) is the information of the target. Please ask the TA or professor if you want to understand this box.

5. The second box (``Results``) is the ephemeris. 

   * You may see some rows like ``>..... Elevation Cut-off Requested .....<`` etc. That means, although the ephemeris was calculated, the target is below the cut-off elevation. Same goes true for ``Daylight Cut-off Requested``. 

   * The explanation of each column is at the bottom of the web site. It can be difficult to understand for beginners, so ask TA or professor if you have questions.

   * Few important columns are the first one (Date), ``T-mag``, ``Azi_(a-appr)_Elev `` (the apparent azimuth and elevation). The ``T-mag`` is kind of a rough estimate of the magnitude of the comet.

   * For the ``Date`` column, you may see some columns that contains ``N``, ``m``, and so on. At the bottom of the web site, the meanings are explained:

     > ```
     > SOLAR PRESENCE (OBSERVING SITE)
     >   Time tag is followed by a blank, then a solar-presence symbol:
     >
     >         '*'  Daylight (refracted solar upper-limb on or above apparent horizon)
     >         'C'  Civil twilight/dawn
     >         'N'  Nautical twilight/dawn
     >         'A'  Astronomical twilight/dawn
     >         ' '  Night OR geocentric ephemeris
     >
     > LUNAR PRESENCE (OBSERVING SITE)
     >   The solar-presence symbol is immediately followed by a lunar-presence symbol:
     >
     >         'm'  Refracted upper-limb of Moon on or above apparent horizon
     >         ' '  Refracted upper-limb of Moon below apparent horizon OR geocentric
     >              ephemeris
     > ```




**Way 2** (not working...)

As we did in the lecture note, we can use ``astroquery.jplhorizons`` module. Since all the known comets  (only < 500 are known **periodic** comets) have known orbital elements, what we can do is just query the ephemerides of all those comets.

The name of the comets can be found at [IAUMPC](https://www.minorplanetcenter.net/iau/lists/PeriodicCodes.html). What you can do is something like this:

```python
from astroquery.jplhorizons import Horizons
# Load the file containing all the comet names
# Put the code in the bottom to a for loop such as ``for id in all_comet_names:``
obj = Horizons(id='C/2016 R2',
               location="37.4539,126.953,0.1",
               epochs=dict(start='2018-04-11T00:00', stop='2018-06-01T00:00', step='1h'))
obj_ephem = obj.ephemerides()
# add code to save the ephemeris.
```

* How to set ``location`` if no MPC observatory code is given? According to p.15 of [HORIZONS_Doc](ftp://ssd.jpl.nasa.gov/pub/ssd/Horizons_doc.pdf), you can set it by ``"<E-long>,<lat>,<h>"``, where ``E-long`` is the longitude in east way (deg), ``lat`` is the latitude (deg), and ``h`` is the altitude above the reference ellipsoid (km).
* SNU 45-dong is roughly ``"126.953,37.4539,0.1"``.
* NOTE: I found this kind of location input does not work. I cannot understand why...