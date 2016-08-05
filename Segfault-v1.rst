
.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

The purpose of this algorithm is to crash mantid. Do **not** run it
unless you want that to happen. This runs a variation the example code
on `wikipedia <https://en.wikipedia.org/wiki/Segmentation_fault>`_.

This cannot be unit-tested for it's actual purpose, as it causes undefined behaviour.

Usage
-----

.. testcode:: SaveMask

    Segfault(DryRun=True)
    
    print "Dry run, did not crash"

Output:

.. testoutput:: SaveMask

    Dry run, did not crash
