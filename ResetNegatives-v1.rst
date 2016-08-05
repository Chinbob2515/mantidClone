.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

This algorithm will search through the input workspace for values less
than zero and make them positive according to the properties. If
``AddMinimum`` is "true" then all values will have :math:`-1*min` for the
spectrum added to them if the minimum is less than zero. Otherwise all
values that are less than zero will be set to ``ResetValue`` which has a
default of 0.

.. testcode:: RebinToWorkspace

   import numpy
   
   ws = CreateSampleWorkspace()
   
   y_values = ws.readY(0)
   
   y_values  = numpy.concatenate([[y_values[0]],[-100],y_values[2:]])
   
   ws.setY(0, y_values)
   
   out = ResetNegatives(InputWorkspace=ws, AddMinimum=False, ResetValue=20)
   
   print "y 0,1:", out.readY(0)[1]
    
.. testcleanup:: RebinToWorkspace

   DeleteWorkspace(ws)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: RebinToWorkspace

   y 0,1: 20.0

.. categories::

.. sourcelink::
