.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Takes a :ref:`WorkspaceGroup <WorkspaceGroup>` as input and ungroups it
into several workspaces. You can perform this from the MantidPlot GUI by
selecting the WorkspaceGroup and clicking "Ungroup".


Usage
-----

.. testcode:: SaveMask

    ws = CreateWorkspace([0],[-10])
    ws1 = CreateWorkspace([1],[123])
    
    gws = GroupWorkspaces([ws, ws1])
    
    UnGroupWorkspace(gws)
    
    sum = 0
    
    for i in range(ws1.getNumberHistograms()): # Just sum ALL the values (so 0+-10+1+123)
        for n in ws1.readY(i):
            sum+=n
            
    for i in range(ws.getNumberHistograms()):
        for n in ws.readY(i):
            sum+=n
    
    print "Sum is", sum




.. testcleanup:: SaveMask

    DeleteWorkspace(ws)
    DeleteWorkspace(ws1)

Output:

.. testoutput:: SaveMask

    Sum is 113.0

.. categories::

.. sourcelink::
