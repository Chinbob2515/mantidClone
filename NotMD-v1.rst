.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Perform the Not (negation) boolean operation on a
:ref:`MDHistoWorkspace <MDHistoWorkspace>`. The not operation is performed
element-by-element. Any 0.0 signal is changed to 1.0 (meaning true). Any
non-zero signal is changed to 0.0 (meaning false).

Usage
-----

.. testcode:: NotMD

   ws = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   out = NotMD(InputWorkspace=ws)
   
   print "Signal (1)(0):", ws.signalAt(0)
   print "Signal (1)(1):", ws.signalAt(1)
   print "Signal (result)(0):", out.signalAt(0)
   print "Signal (result)(1):", out.signalAt(1)

.. testcleanup:: NotMD

   DeleteWorkspace(ws)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: NotMD

   Signal (1)(0): 0.0
   Signal (1)(1): 1.0
   Signal (result)(0): 1.0
   Signal (result)(1): 0.0

.. categories::

.. sourcelink::
