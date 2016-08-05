.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Clones the input :ref:`Matrix Workspaces <MatrixWorkspace>` and orders the
x-axis in an ascending fashion. Ensures that the y-axis and error data
is sorted in a consistent way with the x-axis. All x-values of the input
workspace MUST be in either a descending or ascending fashion before
passing to this algorithm.

This algorithm is for use with small workspaces loaded. It is
particularly suitable for reformatting workspaces loaded via
:ref:`LoadAscii <algm-LoadAscii>`. Input workspaces must be a distribution.

Usage
-----

.. testcode:: SaveMask

    ws = CreateWorkspace(range(5)[::-1], range(5)[::-1])
    
    out = SortXAxis(InputWorkspace = ws)
    
    print "x values:"
    for i in range(out.getNumberHistograms()):
        for n in out.readX(i):
            print n,
    print 




.. testcleanup:: SaveMask

    DeleteWorkspace(ws)
    DeleteWorkspace(out)

Output:

.. testoutput:: SaveMask

    x values:
    0.0 1.0 2.0 3.0 4.0


.. categories::

.. sourcelink::
