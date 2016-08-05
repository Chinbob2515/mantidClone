.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Multiply two :ref:`MDHistoWorkspace <MDHistoWorkspace>`'s or a
MDHistoWorkspace and a scalar.

The error of :math:`f = a * b` is propagated with
:math:`df^2 = f^2 * (da^2 / a^2 + db^2 / b^2)`

-  **MDHistoWorkspace \* MDHistoWorkspace**

   -  The operation is performed element-by-element.

-  **MDHistoWorkspace \* Scalar** or **Scalar \* MDHistoWorkspace**

   -  Every element of the MDHistoWorkspace is multiplied by the scalar.

-  **`MDEventWorkspace <http://www.mantidproject.org/MDEventWorkspace>`_'s**

   -  This operation is not supported, as it is not clear what its
      meaning would be.


Usage
-----

.. testcode:: MultiplyMD

   ws = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws1 = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws.setTo(2,2,3)
   ws1.setTo(4,5,7)
   out = MultiplyMD(LHSWorkspace='ws', RHSWorkspace='ws1')
   
   print "Signal (1):", ws.signalAt(0)
   print "Signal (2):", ws1.signalAt(0)
   print "Signal (result):", out.signalAt(0)


    
.. testcleanup:: MultiplyMD

   DeleteWorkspace(ws)
   DeleteWorkspace(ws1)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: MultiplyMD

   Number of events (1): 2.0
   Number of events (2): 4.0
   Number of events (result): 8.0


.. categories::

.. sourcelink::
