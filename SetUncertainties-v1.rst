.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

The uncertainties for the entire workspace will be recalculated according to the ``SetError`` property.

- ``SetError="zero"`` will change all of the uncertainties to zero
- ``SetError="sqrt"`` will recalculate all of the uncertainties to be the square root of the y value
- ``SetError="oneIfZero"`` will change the uncertainties to one if they are currently zero
- ``SetError="sqrtOrOne"`` will recalculate all of the uncertainties to be the square root of the y value. If the uncertainty is zero it will be set to one.

The result is a ``Workspace2D`` (:py:obj:`mantid.api.MatrixWorkspace`).

Usage
-----

.. testcode:: SetUncertainties

    import numpy
    
    ws = CreateWorkspace([0,1,2,3,4],[0,1,2,3,4])
    
    ws.setE(0, numpy.array([0,1,2,3,4])) # Set errors to be non-zero values
    
    out = SetUncertainties(InputWorkspace = ws)
    
    allZero = True
    for i in range(out.getNumberHistograms()):
        for n in out.readE(i):
            allZero = allZero and n == 0.0
    
    print "Are all zero:", allZero



.. testcleanup:: SetUncertainties

    DeleteWorkspace(ws)
    DeleteWorkspace(out)

Output:

.. testoutput:: SetUncertainties

    Are all zero: True

.. categories::

.. sourcelink::
