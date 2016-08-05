.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Simulate a USANS workspace. This algorithm is used to test the USANS
reduction during development while no real data is available.

A matrix workspace is created for a given analyzer angle. A list of
wavelength peaks coming out of the monochromator can be specified. The
width of those peaks can also be specified.

Both the main detector and the transmission detector are filled with
compatible signals according to a dummy transmission curve.

The amplitude of the signal in the main detector is given by a sphere
model.

A monitor workspace is created with a fake beam profile.

**Note**: This algorithm can take a very long time to execute and is
of limited use for non-developers.

Usage
-----

.. testcode:: USANSSimulation

   USANSSimulation(MonitorWorkspace="monitor", OutputWorkspace="ws") # Very. Incredibly. Slow
   
   ws = mtd["ws"] # Value returned by algorithm and returned by this are different. (e.g. ws = USANSSimulation(...))
   monitor = mtd["monitor"]
   
   print "Workspace title:", ws.getTitle()
   print "Monitor workspace name:", monitor.name()

.. testcleanup:: USANSSimulation

   DeleteWorkspace(ws)
   DeleteWorkspace(monitor)

**Output:**

.. testoutput:: USANSSimulation

   Workspace title: Simulated USANS
   Monitor workspace name: monitor

.. categories::

.. sourcelink::
