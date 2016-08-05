.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

Extracts run parameters from the :ref:`RAW <Raw File>` file given as an
input property. If the ``GetRunParameters`` argument is ``True`` then a
`TableWorkspace <http://www.mantidproject.org/TableWorkspace>`__ is created that contains a 
column for each value of the ``RPB_STRUCT``, i.e. column names such as ``r_dur``, ``r_goodfrm``
etc. This is Mantid's version of the ``Get`` routine in `Open Genie <http://www.opengenie.org/>`__.

.. testcode:: RawFileInfo

   output = RawFileInfo("MAR11060.raw")
   
   print "Instrument info:", output[0]

**Output:**

.. testoutput:: RawFileInfo

   Instrument info: Vanadium white beam                              jaws=50x50 nim=50 dsc=0

.. categories::

.. sourcelink::
