.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

The workspace data are stored in the file in columns: the first column
contains the X-values, followed by pairs of Y and E values. Columns are
separated by spaces. This is used by the reflectometry interface.

Usage
-----

.. testcode:: SaveMask

    import os
    
    ws = Load("MAR11060.raw")
    
    saveFile = os.path.join(os.path.expanduser("~"), "out")
    
    output = SaveReflThreeColumnAscii(InputWorkspace=ws, Filename=saveFile)
    
    print "File exists:", os.path.exists(saveFile)



.. testcleanup:: SaveMask

    os.remove(savefile)
    DeleteWorkspace(ws)

Output:

.. testoutput:: SaveMask

    File Exists: True

.. categories::

.. sourcelink::
