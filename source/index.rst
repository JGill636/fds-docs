.. FDS online documentation master file, created by
   sphinx-quickstart on Thu May 25 10:07:05 2023.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to FDS online documentation!
====================================

**Fire Dynamics Simulator (FDS)** is a computational fluid dynamics (CFD) model of fire-driven fluid flow.

* Hi this should be a bullet
* This as well but it will have
  multiple lines

1. numbered
2. list

Does this work? :eq:`euler2`

.. contents:: Table of Contents
   

#. hi
#. hi

.. math::
   (a + b)^2 = a^2 + 2ab + b^2

   (a - b)^2 = a^2 - 2ab + b^2

.. math::
   :label: euler

   e^{i\pi} + 1 = 0

.. math::
   :label: slope

   y = mx + b

.. math::
   :label: eq2

   (a + b)^2  &=  (a + b)(a + b) \\&=  a^2 + 2ab + b^2

.. math::
   :label: eq3

   (a + b)^2 = a^2 + 2ab + b^2

.. math::
   :label: eq4

   \begin{eqnarray}
      y    & = & ax^2 + bx + c \\
      f(x) & = & x^2 + 2xy + y^2
   \end{eqnarray}

New Section
===========

Euler's identity, equation :eq:`euler`, was elected one of the most
beautiful mathematical formulas.

Calling my slope formula from the same file, :eq:`Slope <slope>`

term (up to a line of text)
   Definition of the term, which must be indented

   and can even consist of multiple paragraphs

next term
   Description.

**Adding more content to just to fill in the page**

**Inline text math example:**
In physics, the mass-energy equivalence is stated 
by the equation :math:`E=mc^2`, discovered in 1905 by Albert Einstein.

**more inline text math example:**
Subscripts in math mode are written as $a_b$ and superscripts are written as $a^b$. These can be combined and nested to write expressions such as
:math:`T^{i_1 i_2 \dots i_p}_{j_1 j_2 \dots j_q}`, some text after

The needle is composed of two materials—’dry pine’ and ’MOISTURE’. Following the convention used
in forestry, the moisture content is expressed via the MOISTURE_FRACTION, which is the mass of moisture
divided by the mass of dry vegetation. Do not confuse this with the mass fraction of moisture, Ym, which is
related to the moisture fraction, M, via

adding some text
.. note::

   This project is under active development.


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

Contents
--------

.. toctree::
   :numbered:
   :maxdepth: 2

   usage
   test1
