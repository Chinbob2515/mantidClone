.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

This algorithm is only used for testing.


Usage
-----

.. testcode:: TestGroupWorkspaceProperty

   ws = CreateSampleWorkspace(Function='Powder Diffraction')
   gws = GroupWorkspaces([ws])
   
   ws1 = CreateWorkspace([0],[1])
   ws2 = CreateWorkspace([2],[3])
   gws1 = GroupWorkspaces([ws1,ws2])
   
   output = TestWorkspaceGroupProperty(gws,gws1)
   
   print output # Doesn't throw an error I guess

.. testcleanup:: TestGroupWorkspaceProperty

   DeleteWorkspace(ws)
   DeleteWorkspace(ws1)
   DeleteWorkspace(ws2)
   DeleteWorkspace(gws)
   DeleteWorkspace(gws1)

**Output:**

.. testoutput:: TestGroupWorkspaceProperty

   None

.. categories::

.. sourcelink::
