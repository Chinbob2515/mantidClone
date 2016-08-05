.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

**This algorithm is meant for developers only!**

This algorithm is used for performance testing and debugging of nexus
saving and loading.

If you specify ``SaveFilename`` (optional), then the algorithm will save a
file with the given number of chunks of the given size.

If you specify ``LoadFilename`` (optional), then the algorithm will load
back a file created with this algorithm.

The ``SaveSpeed`` and ``LoadSpeed`` output properties are set to the saving
and loading rates, in MB per second.

Usage
-----
.. testcode:: NexusTester

   speeds = NexusTester(SaveFilename="bob.nxs")

   print speeds[0]+speeds[1]+speeds[2]>0 # File writing/reading speeds- should be above 0mb/s.

**Output:**

.. testoutput:: NexusTester

   True

.. categories::

.. sourcelink::
