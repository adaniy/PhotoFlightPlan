photoflightplan.py
A photographic flight plan generation software for manned aircrafts
by André Verville, Kildir Technologies
-------------------------------------------------------------------

Overview:
---------
There are many photographic flight plan generation programs that are provided
by UAV equipments providers or or also from the open source community.
A good example of the second type is the excellent Mission Planner software
from Michael Oborne that provides many options for UAV grid-based photographic
surveys using automated waypoints navigation.

Recently involved producing the same kind of aerial photo coverages for manned
aerial aircrafts, we have found that commercial software is expensive, complex
and most often relies on Windows-based environments and proprietary equipments.
Although there may exist some, we have found nothing that could be open, free
and inexpensive to build and use. PhotoFlightPlan is provided under a GPL license,
it is free to use and modify by the aerial photography industry.

Photogrammetry requirements are universal and pretty straightfoward but manned
aircrafts have their own requirements that differ from fixed and rotating wings UAVs.
Amongst them, the flying altitude constraint that can be imposed by flight traffic
control. There is also the pilots’ natural preference of flying upwind to minimize
ground speed and limit yaw and direction corrections that induce roll movements to
the aircraft. Those constraints make it such that often, there is a need to recompute
the flight planning at the last minute.

After a few interactive flight plannings where I used Mission Planner to compute
waypoints, then copy/paste them to text files and reformat/export the latitudes and
longitudes to Google Earth and a GPS-based flight navigation assistant I have built,
called Collimator, I decided that the time had come to automate the generation of those
flight plans. I built photoflightplan.py for this purpose, bearing in mind that it
needs to be simple, straightforward but also rigorous, photogrammetrically speaking.
For now, it is a rather simple « terminal » based application. I will work out a GUI
wrapper that shall make it even easier to use in this all-web era. In practice, a
Web service could be developed quite easily around it. Anyhow, Python is simple to use
and most of all, it is either already pre-installed or can be installed easily and
freely on most computers. There is even a version for IOS, called Pythonista that makes
photoflightplan.py something someone can use on an iPhone or iPad. Too bad folks,
it costs a few dollars there :-(

The reader should bear in mind that the flight plan generated by photoflightplan.py
is meant to produce a data file that can also be used as input by the Collimator
flight navigation assist system (another parent project). Collimator requires special
equipment to be used onboard an aircraft (Raspberry Pi computer, GPS, display and
control unit, color LED strip) but the acquisition cost of the equipment is just a few
hundreds of dollars, which is almost nothing in this world of aircraft-grade systems.

Characteristics:
----------------
Python 3 based, can be executed on any platform, even on an IOS iPhone or iPad
(Pythonista IOS app required).

Takes all its operating parameters from a user-created text file named
« photoflightplan.par ». An example parameters file is provided in the software package.

The user provides the AOI (Area Of Interest) polygon points in latitudes and longitudes
within the parameters file or else provides the name of kml files that contains these
polygons (one kml per AOI polygon).

PhotoFlightPlan takes camera parameters for any camera model, but the user needs to
know and provide specific parameters values of his/her camera: focal length, sensor
size and number of pixels on each axis.

The user provides overlap and sidelap as percentages of the image size in each
direction, where overlap is measured along the flying line and sidelap across it
towards the other flight lines. These values are critical for photogrammetric image
processing software packages like Pix4Dmapper or PhotoScan and are generally either
imposed or suggested by the image processing software or past experience with a certain
type of coverage (urban, agricultural, forest, etc).

The flight lines are oriented towards (upwind) the provided wind direction, with entry
point computed downwind. This is the simplest way of imposing flight lines orientation
to PhotoFlightPlan.

Multiple AOIs can be specified, PhotoFlightPlan generates a flight block for each of
them. The same AOI can also be provided many times, each with a different wind direction.
PhotoFlightPlan will then generate many flight blocks, each with a different flight line
orientation.

PhotoFlightPlan generates a kml file (photoflightplan.kml) that can be used to quickly
visualize the results on Google Earth (all platforms).

PhotoFlightPlan also generates a .pfp (photo flight plan) file that summarizes all
project info and serves as input to the Collimator flight navigation assistant.
