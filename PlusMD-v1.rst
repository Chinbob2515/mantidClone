.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

This algorithm sums two :ref:`MDHistoWorkspaces <MDHistoWorkspace>` or
merges two `MDEventWorkspaces <http://www.mantidproject.org/MDEventWorkspace>`_ together.

MDHistoWorkspaces
#################

-  **MDHistoWorkspace + MDHistoWorkspace**

   -  The operation is performed element-by-element.

-  **MDHistoWorkspace + Scalar** or **Scalar + MDHistoWorkspace**

   -  The scalar is subtracted from every element of the
      MDHistoWorkspace. The squares of errors are summed.

Usage
-----

.. testcode:: PlusMD1

   ws = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws1 = CreateMDHistoWorkspace(Dimensionality=2,Extents='-3,3,-10,10',SignalInput=range(0,100),ErrorInput=range(0,100),NumberOfBins='10,10',Names='Dim1,Dim2',Units='MomentumTransfer,EnergyTransfer')
   ws.setTo(2,2,3)
   ws1.setTo(4,5,7)
   out = PlusMD(LHSWorkspace='ws', RHSWorkspace='ws1')
   
   print "Signal (1):", ws.signalAt(0)
   print "Signal (2):", ws1.signalAt(0)
   print "Signal (result):", out.signalAt(0)


.. testcleanup:: PlusMD1

   DeleteWorkspace(ws)
   DeleteWorkspace(ws1)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: PlusMD1

   Signal (1): 2.0
   Signal (2): 4.0
   Signal (result): 6.0

MDEventWorkspaces
#################

This algorithm operates similary to calling Plus on two
:ref:`EventWorkspaces <EventWorkspace>`: it combines the events from the
two workspaces together to form one large workspace.

Usage
-----

.. testcode:: PlusMD2

   ws = CreateMDWorkspace(Dimensions=2, Extents='1,5,1,4', Names='x,y', Units='Wavelength,Spectrum', OutputWorkspace='ws')
   FakeMDEventData(InputWorkspace='ws', UniformParams='3')
   ws1 = CreateMDWorkspace(Dimensions=2, Extents='-1,4,-1,6', Names='x,y', Units='Wavelength,Spectrum', OutputWorkspace='ws1')
   FakeMDEventData(InputWorkspace='ws1', UniformParams='2')
   
   out = PlusMD(LHSWorkspace='ws', RHSWorkspace='ws1')
   
   print "Events (1):", ws.getNEvents()
   print "Events (2):", ws1.getNEvents()
   print "Events (result):", out.getNEvents()


.. testcleanup:: PlusMD2

   DeleteWorkspace(ws)
   DeleteWorkspace(ws1)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: PlusMD2

   Events (1): 3
   Events (2): 2
   Events (result): 4

Note for file-backed workspaces
###############################

The algorithm uses :ref:`algm-CloneMDWorkspace` to create the
output workspace, except when adding in place (e.g. :math:`A = A + B` ).
See :ref:`algm-CloneMDWorkspace` for details, but note that a
file-backed `MDEventWorkspace <http://www.mantidproject.org/MDEventWorkspace>`_ will have its file
copied.

-  If A is in memory and B is file-backed, the operation
   :math:`C = A + B` will clone the B file-backed workspace and add A to
   it.
-  However, the operation :math:`A = A + B` will clone the A workspace
   and add B into memory (which might be too big!)

Also, be aware that events added to a MDEventWorkspace are currently
added **in memory** and are not cached to file until :ref:`algm-SaveMD`
or another algorithm requiring it is called. The workspace is marked as
'requiring file update'.

.. categories::

.. sourcelink::
