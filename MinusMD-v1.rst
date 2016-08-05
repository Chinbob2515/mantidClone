.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Subtract two :ref:`MDHistoWorkspace <MDHistoWorkspace>`'s or a
MDHistoWorkspace and a scalar.

-  **MDHistoWorkspace - MDHistoWorkspace**

   -  The operation is performed element-by-element.

-  '''MDHistoWorkspace - Scalar '''

   -  The scalar is subtracted from every element of the
      MDHistoWorkspace. The squares of errors are summed.

-  **Scalar - MDHistoWorkspace**

   -  This is not allowed.

-  **`MDEventWorkspace <http://www.mantidproject.org/MDEventWorkspace>`_ -
   `MDEventWorkspace <http://www.mantidproject.org/MDEventWorkspace>`_**

   -  The signal of each event on the right-hand-side is multiplied by
      -1 before the events are summed.
   -  The number of events in the output MDEventWorkspace is that of the
      LHS and RHS workspaces put together.

-  **`MDEventWorkspace <http://www.mantidproject.org/MDEventWorkspace>`_ - Scalar or
   MDHistoWorkspace**

   -  This is not possible.


Usage
-----

.. testcode:: MinusMD

   ws = CreateMDWorkspace(Dimensions=2, Extents='1,5,1,4', Names='x,y', Units='Wavelength,Spectrum', OutputWorkspace='ws')
   FakeMDEventData(InputWorkspace='ws', UniformParams='3')
   ws1 = CreateMDWorkspace(Dimensions=2, Extents='-1,4,-1,6', Names='x,y', Units='Wavelength,Spectrum', OutputWorkspace='ws1')
   FakeMDEventData(InputWorkspace='ws1', UniformParams='2')
   
   out = MinusMD(LHSWorkspace='ws', RHSWorkspace='ws1', OutputWorkspace='out')
   
   print "Number of events (1):", ws.getNEvents()
   print "Number of events (2):", ws1.getNEvents()
   print "Number of events (result):", out.getNEvents()

    
.. testcleanup:: MinusMD

   DeleteWorkspace(ws)
   DeleteWorkspace(ws1)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: MinusMD

   Number of events (1): 3
   Number of events (2): 2
   Number of events (result): 4

.. categories::

.. sourcelink::
