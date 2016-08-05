.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

This algorithm is meant to merge a large number of large
MDEventWorkspaces together into one file-backed MDEventWorkspace,
without exceeding available memory.

First, you will need to generate a MDEventWorkspaces NXS file for each
run with a fixed box structure:

-  You can call :ref:`algm-CreateMDWorkspace` with
   MinRecursionDepth = MaxRecursionDepth.

   -  This will make the box structure identical. The number of boxes
      will be equal to SplitInto ^ (NumDims \* MaxRecursionDepth).
   -  Aim for the boxes to be small enough for all events contained to
      fit in memory; without there being so many boxes as to slow down
      too much.

-  This can be done immediately after acquiring each run so that less
   processing has to be done at once.

Then, enter the path to all of the files created previously. The
algorithm avoids excessive memory use by only keeping the events from
ONE box from ALL the files in memory at once to further process and
refine it. This is why it requires a common box structure.

See also: :ref:`algm-MergeMD`, for merging any MDWorkspaces in system
memory (faster, but needs more memory).


Usage
-----

.. testcode:: MergeMDFiles

   locations = [os.path.join(os.path.expanduser("~"), "ws.nxs"), os.path.join(os.path.expanduser("~"), "ws1.nxs"), os.path.join(os.path.expanduser("~"), "many.nxs")]
   ws = CreateMDWorkspace(Dimensions=3, Extents='-10,10,-10,10,-10,10', Names='1,2,3', Units='Wavelength,Wavelength,Wavelength')
   FakeMDEventData(ws, range(1, 8))
   ws1 = CreateMDWorkspace(Dimensions=3, Extents='-10,10,-10,10,-10,10', Names='1,2,3', Units='Wavelength,Wavelength,Wavelength')
   FakeMDEventData(ws1, range(1, 8))
   FakeMDEventData(ws1, range(1, 8))

   print "ws no of events:", ws.getNEvents()
   print "ws1 no of events:", ws1.getNEvents()
   
   SaveMD(InputWorkspace=ws, Filename=locations[0])
   SaveMD(InputWorkspace=ws1, Filename=locations[1])
   
   out = MergeMDFiles(locations[0]+", "+locations[1], OutputFileName=locations[2])
   
   print "out no of events:", out.getNEvents()

.. testcleanup:: MergeMDFiles

   DeleteWorkspace(ws)
   DeleteWorkspace(ws1)
   DeleteWorkspace(out)
   import os
   for name in locations: os.remove(name)

**Output:**

.. testoutput:: MergeMDFiles

   ws no of events: 1
   ws1 no of events: 2
   out no of events: 3

.. categories::

.. sourcelink::
