.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

This algorithm rebins a 2D workspace in units of wavelength into 2D Q.
The reduction it performs is the same as that executed by the
:ref:`algm-Q1D` algorithm, expect performed in 2D instead of 1D. Hence,
for further documentation on how this algorithm works please see
:ref:`algm-Q1D`.

.. testcode:: Qxy

   ws = CreateSampleWorkspace(WorkspaceType="Histogram",Function="One Peak", XUnit="Wavelength")
   
   out = Qxy(InputWorkspace=ws, MaxQxy=1e-12, DeltaQ=1e-12, OutputWorkspace="out")
   
   print "x 0,0:", out.readX(0)[0]
   print "x 0,1:", out.readX(0)[1]
   print "x 1,0:", out.readX(1)[0]
   print "x 1,1:", out.readX(1)[1]
    
.. testcleanup:: Qxy

   DeleteWorkspace(ws)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: Qxy

   x 0,0: -1e-12
   x 0,1: 0.0
   x 1,0: -1e-12
   x 1,1: 0.0

.. categories::

.. sourcelink::
