.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

This executes the power function on a :ref:`MDHistoWorkspace <MDHistoWorkspace>`.

The signal :math:`a` becomes :math:`f = a^b`

The error :math:`da` becomes :math:`df^2 = f^2 * b^2 * (da^2 / a^2)`

This algorithm cannot be run on a
`MDEventWorkspace <http://www.mantidproject.org/MDEventWorkspace>`__. Its equivalent on a
:ref:`MatrixWorkspace <MatrixWorkspace>` is called :ref:`algm-Power`.

Usage
-----

.. testcode:: PowerMD

   ws = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws.setTo(2,3,4)
   
   out = PowerMD(InputWorkspace = ws)
   
   print "Signal (1)", ws.signalAt(0)
   print "Signal (result)", out.signalAt(0)


.. testcleanup:: PowerMD

   DeleteWorkspace(ws)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: PowerMD

   Signal (1) 2.0
   Signal (result) 4.0

.. categories::

.. sourcelink::
