.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

This is a custom save method as there is the ability to customise the headers, including adding log lists and subtitles as required.
The workspace data are stored in the file in columns: the first column
contains the X-values, followed by pairs of Y and E values. There is an optional fourth column of Delta Q values. Columns are
separated by spaces. This is used by the reflectometry interface.

Usage
-----

.. testcode:: SaveMask

    import os
    
    ws = Load("MAR11060.raw")
    
    saveFile = os.path.join(os.path.expanduser("~"), "out")
    
    output = SaveReflCustomAscii(InputWorkspace=ws, Filename=saveFile)
    
    print "File exists:", os.path.exists(saveFile)



.. testcleanup:: SaveMask

    os.remove(savefile)
    DeleteWorkspace(ws)

Output:

.. testoutput:: SaveMask

    File Exists: True


.. categories::

.. sourcelink::
