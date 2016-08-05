.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

This algorithm Corrects the time of flight (TOF) of an indirect geometry
instrument by substracting a time offset :math:`t_0` linearly dependent
on the wavelenght of the neutron when emitted through the moderator.
This algorithm is suitable to data reduction of indirect instruments
featuring a neutron flux with a narrow distribution of wavelenghts. A
empirical formula for the correction, stored in the instrument
definition file, is taken as linear on the initial neutron wavelength
:math:`\lambda_i`: :math:`t_0 = a * \lambda_i + b`,
(:math:`a` is in units of microsec/Angstrom and :math:`a` is in units 
of microsec. Below is the example XML code included in BASIS beamline 
parameters file.

.. code-block:: xml

    <!-- Moderator Tzero/LambdaZero Parameters  -->
    <parameter name="Moderator.TimeZero.Gradient">
        <value val="11.967"/>
    </parameter>
    <parameter name="Moderator.TimeZero.Intercept">
        <value val="-5.0"/>
    </parameter>

The recorded TOF: :math:`TOF = t_0 + t_i + t_f`, with

-  :math:`t_0`: emission time from the moderator
-  :math:`t_i`: time from moderator to sample
-  :math:`t_f`: time from sample to detector

This algorithm will replace TOF with :math:`TOF' = TOF-t_0 = t_i + t_f`

For an indirect geometry instrument, :math:`\lambda_i` is not known but
the final energy, :math:`E_f`, selected by the analyzers is known. For
this geometry:

-  :math:`t_f = L_f/v_f`, with :math:`L_f`: distance from sample to
   detector, :math:`v_f`: final velocity derived from :math:`E_f`
-  :math:`t_i = L_i/v_i`, with :math:`L_i`: distance from moderator to
   sample, :math:`v_i`: initial velocity unknown
-  :math:`t_0 = a'/v_i+b'`, with :math:`a'` and :math:`b'` constants derived from the
   aforementioned empirical formula
   :math:`a' = a \cdot 3.956 \cdot 10^{-3}` with :math:`a'` in units of meters

and :math:`b' = b` with :math:`b'` in units of microseconds.

Putting all together:
:math:`TOF' = \frac{L_i}{L_i+a'} \cdot (TOF-t_f-b') + t_f`, with
[TOF']=microsec

If the detector is a monitor, then we can treat it as both sample and
detector. Thus, we use the previous formula inserting the time from
sample to detector :math:`t_f = 0` and with the initial fligh path
:math:`L_i` as the distance from source to monitor.

Usage
-----

.. testcode:: ModeratorTzeroLinear

   ws = CreateSampleWorkspace(WorkspaceType="Histogram",Function="One Peak")
   LoadInstrument(Workspace=ws, Filename=os.path.join(config.getInstrumentDirectory(), "BASIS_Definition_20140101-.xml"), MonitorList='-1', RewriteSpectraMap='True')
   out = ModeratorTzeroLinear(InputWorkspace=ws)
   
   print "ws x 0,0:", ws.readX(0)[0] # just read out some random values to check
   print "ws x 0,1:", ws.readX(0)[1]
   print "ws x 1,0:", ws.readX(1)[0]
   print "ws x 1,1:", ws.readX(1)[1]
   print "out x 0,0:", out.readX(0)[0]
   print "out x 0,1:", out.readX(0)[1]
   print "out x 1,0:", out.readX(1)[0]
   print "out x 1,1:", out.readX(1)[1]

.. testcleanup:: ModeratorTzeroLinear

   DeleteWorkspace(ws)
   DeleteWorkspace(out)

**Output:**

.. testoutput:: ModeratorTzeroLinear

   ws x 1,0: 0.0
   ws x 1,1: 200.0
   out x 0,0: 4.9971757672
   out x 0,1: 204.884206455
   out x 1,0: 9.21650800894
   out x 1,1: 209.10385279

.. categories::

.. sourcelink::
