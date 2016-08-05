.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Iterates over the input workspace evaluating the test for each single
value spectrum. If the detectors should be masked it deselects all of
the contributing detectors in the output calfile. All other aspects of
the ``InputCalFile`` are copied over to the ``OutputCalFile``.

Usage
-----

.. testcode:: MaskDetectorsIf

   ws = CreateWorkspace([1],[0])
   Output = MaskDetectorsIf(InputWorkspace=ws, InputCalFile="hrpd_new_072_01_corr.cal", OutputCalFile="newCalFile.cal")
   print "No output-", Output
    
.. testcleanup:: MaskDetectorsIf

   DeleteWorkspace(ws)

**Output:**

.. testoutput:: MaskDetectorsIf

   No output- None

.. categories::

.. sourcelink::
