.. algorithm::

.. summary::

.. alias::

.. properties::

Description
-----------

This algorithm fits a spectrum to a user defined function. The function
is supplied to the algorithm as a text string. The function here is a
mathematical expression using numbers, variable names and internal
function names. Symbols '+', '-', '\*', '/', and '^' can be used for
arithmetic operations. Names can contain only letters, digits, and the
underscore symbol '\_'. The internal functions are:

+---------+---------+-------------------------------------+
| Name    | Argc.   | Explanation                         |
+=========+=========+=====================================+
| sin     | 1       | sine function                       |
+---------+---------+-------------------------------------+
| cos     | 1       | cosine function                     |
+---------+---------+-------------------------------------+
| tan     | 1       | tangens function                    |
+---------+---------+-------------------------------------+
| asin    | 1       | arcus sine function                 |
+---------+---------+-------------------------------------+
| acos    | 1       | arcus cosine function               |
+---------+---------+-------------------------------------+
| atan    | 1       | arcus tangens function              |
+---------+---------+-------------------------------------+
| sinh    | 1       | hyperbolic sine function            |
+---------+---------+-------------------------------------+
| cosh    | 1       | hyperbolic cosine                   |
+---------+---------+-------------------------------------+
| tanh    | 1       | hyperbolic tangens function         |
+---------+---------+-------------------------------------+
| asinh   | 1       | hyperbolic arcus sine function      |
+---------+---------+-------------------------------------+
| acosh   | 1       | hyperbolic arcus tangens function   |
+---------+---------+-------------------------------------+
| atanh   | 1       | hyperbolic arcur tangens function   |
+---------+---------+-------------------------------------+
| log2    | 1       | logarithm to the base 2             |
+---------+---------+-------------------------------------+
| log10   | 1       | logarithm to the base 10            |
+---------+---------+-------------------------------------+
| log     | 1       | logarithm to the base 10            |
+---------+---------+-------------------------------------+
| ln      | 1       | logarithm to base e (2.71828...)    |
+---------+---------+-------------------------------------+
| exp     | 1       | e raised to the power of x          |
+---------+---------+-------------------------------------+
| sqrt    | 1       | square root of a value              |
+---------+---------+-------------------------------------+
| sign    | 1       | sign function -1 if x<0; 1 if x>0   |
+---------+---------+-------------------------------------+
| rint    | 1       | round to nearest integer            |
+---------+---------+-------------------------------------+
| abs     | 1       | absolute value                      |
+---------+---------+-------------------------------------+
| if      | 3       | if ... then ... else ...            |
+---------+---------+-------------------------------------+
| min     | var.    | min of all arguments                |
+---------+---------+-------------------------------------+
| max     | var.    | max of all arguments                |
+---------+---------+-------------------------------------+
| sum     | var.    | sum of all arguments                |
+---------+---------+-------------------------------------+
| avg     | var.    | mean value of all arguments         |
+---------+---------+-------------------------------------+

An example of *Function* property is "a + b\*x + c\*x^2". Variable *x*
is used to represent the values of the X-vector of the input spectrum.
All other variable names are treated as fitting parameters. A parameter
can be given an initial value in the *InitialParameters* property. For
example, "b=1, c=0.2". The order in which the variables are listed is
not important. If a variable is not given a value, it is initialized
with 0.0. If some of the parameters should be fixed in the fit list them
in the *Fix* property in any order, e.g. "a,c".

The resulting parameters are returned in a
`TableWorkspace <http://www.mantidproject.org/TableWorkspace>`_ set in ``OutputParameters`` property.
Also for displaying purposes *OutputWorkspace* is returned. It contains
the initial spectrum, the fitted spectrum and their difference.

Example
-------

.. figure:: /images/UserFunction1D.gif

In this example the fitting function is a\*exp(-(x-c)^2\*s). The
parameter *s* is fixed.

Usage
-----

.. testcode:: UserFunction1D

   ws = WorkspaceFactory.create("Workspace2D", 3, 10, 10)
   for i in range(3):
       X = ws.dataX(i)
       Y = ws.dataY(i)
       E = ws.dataE(i)           # Build a table
       for j in range(10):
           X[j] = 1.0 * j
           Y[j] = (i+1) * (2.0 + 4 * X[j])
           E[j] = 1.0
   AnalysisDataService.add("ws", ws) # Make mantid aware of it
   
   out = UserFunction1D(InputWorkspace="ws", Function="a+b*x", WorkspaceIndex=0, Output="out")
   
   params = mtd["out_Parameters"]
   keys = params.keys()
   for key in keys:
       i = 0
       for row in params:
           print "row ", i, " column ", key, " : ", row[key]
           i += 1


.. testcleanup:: UserFunction1D

   DeleteWorkspace(ws)
   DeleteWorkspace(out_Workspace)
   DeleteWorkspace(out_Parameters)
   DeleteWorkspace(out_NormalisedCovarianceMatrix)

**Output:**

.. testoutput:: UserFunction1D

   row  0  column  Name  :  Chi^2/DoF
   row  1  column  Name  :  a
   row  2  column  Name  :  b
   row  0  column  Value  :  2.46519032882e-32
   row  1  column  Value  :  2.0
   row  2  column  Value  :  4.0
   row  0  column  Error  :  0.0
   row  1  column  Error  :  0.587753813645
   row  2  column  Error  :  0.110096376513

.. categories::

.. sourcelink::
