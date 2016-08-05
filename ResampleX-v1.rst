.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

This method will resample the x-axis with the number of specified bins.
This is done by setting up appropriate parameters to call
:ref:`Rebin <algm-Rebin>` with. If the ``XMin`` and ``XMax`` parameters are supplied
it will use those as the range, they can be supplied as a comma delimited
list or as a single value.

The ``LogBinning`` option calculates constant delta-X/X binning and rebins
using that, otherwise the bins are constant width.

.. testcode:: RebinToWorkspace

   ws = CreateWorkspace([2,5],[1,0])
   
   output = ResampleX(ws,NumberBins=1)
   
   print "x 0,0:", output.readX(0)[0]
    
.. testcleanup:: RebinToWorkspace

   DeleteWorkspace(ws)
   DeleteWorkspace(output)

**Output:**

.. testoutput:: RebinToWorkspace

   y 0,0: 3.5


.. categories::

.. sourcelink::
