.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Saves a workspace out to a VTK file that can be loaded with Paraview or
any other software supporting the VTK file format. This is a very basic
algorithm that simple creates a 3D view of the data as a series of
histograms. It should only be used for relatively small data sets as the
resulting file can become quite large relatively quickly.

Usage
-----

.. testcode:: SaveMask

    import os
    
    ws = Load("MAR11060.raw")
    
    saveFile = os.path.join(os.path.expanduser("~"), "out")
    
    output = SaveVTK(InputWorkspace=ws, Filename=saveFile)
    
    saveFile += ".vtu" # Function adds extension on automatically
    
    print "File exists:", os.path.exists(saveFile)



.. testcleanup:: SaveMask

    os.remove(savefile)
    DeleteWorkspace(ws)

Output:

.. testoutput:: SaveMask

    File Exists: True

.. categories::

.. sourcelink::
