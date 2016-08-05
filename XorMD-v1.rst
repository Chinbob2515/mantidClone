.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Perform the Xor (exclusive-or) boolean operation on two
MDHistoWorkspaces. The xor operation is performed element-by-element. A
signal of 0.0 or a masked bin means "false" and any non-zero signal is
"true".


Usage
-----

.. testcode:: XorMD1

   ws = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws1 = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws.setTo(0,2,3)
   ws1.setTo(4,5,7)
   out = XorMD(LHSWorkspace='ws', RHSWorkspace='ws1')
   
   print "Signal (1):", ws.signalAt(0)
   print "Signal (2):", ws1.signalAt(0)
   print "Signal (result):", out.signalAt(0)


.. testcleanup:: XorMD1

   DeleteWorkspace(ws)
   DeleteWorkspace(ws1)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: XorMD1

   Signal (1): 0.0
   Signal (2): 4.0
   Signal (result): 1.0

.. testcode:: XorMD2

   ws = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws1 = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws.setTo(2,2,3)
   ws1.setTo(4,5,7)
   out = XorMD(LHSWorkspace='ws', RHSWorkspace='ws1')
   
   print "Signal (1):", ws.signalAt(0)
   print "Signal (2):", ws1.signalAt(0)
   print "Signal (result):", out.signalAt(0)


.. testcleanup:: XorMD2

   DeleteWorkspace(ws)
   DeleteWorkspace(ws1)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: XorMD2

   Signal (1): 2.0
   Signal (2): 4.0
   Signal (result): 0.0

.. testcode:: XorMD3

   ws = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws1 = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws.setTo(0,2,3)
   ws1.setTo(0,5,7)
   out = XorMD(LHSWorkspace='ws', RHSWorkspace='ws1')
   
   print "Signal (1):", ws.signalAt(0)
   print "Signal (2):", ws1.signalAt(0)
   print "Signal (result):", out.signalAt(0)


.. testcleanup:: XorMD3

   DeleteWorkspace(ws)
   DeleteWorkspace(ws1)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: XorMD3

   Signal (1): 0.0
   Signal (2): 0.0
   Signal (result): 0.0

.. categories::

.. sourcelink::
