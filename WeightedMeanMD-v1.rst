.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Takes two MDHistoWorkspaces and calculates the weighted mean for each
bin. See :ref:`algm-WeightedMean` for more details on the
algorithm workings. Both inputs must be MDHistoWorkspaces, the algorithm
will not run with MDEventWorkspaces.


Usage
-----

.. testcode:: WeightedMeanMD

   ws = CreateMDHistoWorkspace(SignalInput=range(0,12), ErrorInput=range(0,12), NumberOfEvents=range(0,12), Dimensionality=2, Extents='-1,-1,2,2', NumberOfBins='3,4', Names='1,1', Units='2,2')
   ws.setTo(1,2,3)
   ws1 = CreateMDHistoWorkspace(SignalInput='6,5,4,3,2,1,6,5,4,3,2,1', ErrorInput='6,5,4,3,2,1,6,5,4,3,2,1', NumberOfEvents='6,5,4,3,2,1,6,5,4,3,2,2', Dimensionality=2, Extents='-1,-1,2,2', NumberOfBins='3,4', Names='1,1', Units='2,2')
   ws1.setTo(4,5,6)
   
   out = WeightedMeanMD(LHSWorkspace = ws, RHSWorkspace=ws1)
   
   print "ws signal at 0:", ws.signalAt(0) # Should be a uniform signal, I think
   print "ws1 signal at 0:", ws1.signalAt(0)
   print "out signal at 0:", out.signalAt(0)

.. testcleanup:: WeightedMeanMD

   DeleteWorkspace(ws)
   DeleteWorkspace(ws1)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: WeightedMeanMD

   ws signal at 0: 1.0
   ws1 signal at 0: 4.0
   out signal at 0: 1.85714285714

.. categories::

.. sourcelink::
