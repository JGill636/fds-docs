.. _label_introduction:
   
************
Introduction
************

.. role:: raw-latex(raw)
   :format: latex
..

The software described in this document, Fire Dynamics Simulator (FDS),
is a computational fluid dynamics (CFD) model of fire-driven fluid flow.
FDS solves numerically a form of the Navier-Stokes equations appropriate
for low-speed (Ma [1]_ < 0.3), thermally-driven flow with an emphasis on
smoke and heat transport from fires. The formulation of the equations
and the numerical algorithm are contained in the FDS Technical Reference
Guide :raw-latex:`\cite{FDS_Math_Guide}`. Verification and Validation of
the model are discussed in the FDS
Verification :raw-latex:`\cite{FDS_Verification_Guide}` and
Validation :raw-latex:`\cite{FDS_Validation_Guide}` Guides.

Smokeview is a separate visualization program that is used to display
the results of an FDS simulation. A detailed description of Smokeview is
found in a separate user’s
guide :raw-latex:`\cite{Smokeview_Users_Guide}`.

Features of FDS
===============

The first version of FDS was publicly released in February 2000. To
date, about half of the applications of the model have been for design
of smoke handling systems and sprinkler/detector activation studies. The
other half consist of residential and industrial fire reconstructions.
Throughout its development, FDS has been aimed at solving practical fire
problems in fire protection engineering, while at the same time
providing a tool to study fundamental fire dynamics and combustion.

Hydrodynamic Model
   FDS solves numerically a form of the Navier-Stokes equations
   appropriate for low-speed, thermally-driven flow with an emphasis on
   smoke and heat transport from fires. The core algorithm is an
   explicit predictor-corrector scheme, second order accurate in space
   and time. Turbulence is treated by means of Large Eddy Simulation
   (LES). It is possible to perform a Direct Numerical Simulation (DNS)
   if the underlying numerical mesh is fine enough. See
   Sec. `[Sim_Mode] <#Sim_Mode>`__ for further details.

Combustion Model
   For most applications, FDS uses a single step, mixing-controlled
   chemical reaction which uses three lumped species (a species
   representing a group of species). These lumped species are air, fuel,
   and products. By default the last two lumped species are explicitly
   computed. Options are available to include multiple reactions and
   reactions that are not necessarily mixing-controlled.

Radiation Transport
   Radiative heat transfer is included in the model via the solution of
   the radiation transport equation for a gray gas, and in some limited
   cases using a wide band model. The equation is solved using a
   technique similar to finite volume methods for convective transport,
   thus the name given to it is the Finite Volume Method (FVM). Using
   approximately 100 discrete angles, the finite volume solver requires
   about 20 % of the total CPU time of a calculation, a modest cost
   given the complexity of radiation heat transfer. The absorption
   coefficients of the gas-soot mixtures are computed using the RadCal
   narrow-band model :raw-latex:`\cite{RadCal}`. Liquid droplets can
   absorb and scatter thermal radiation. This is important in cases
   involving mist sprinklers, but also plays a role in all sprinkler
   cases. The absorption and scattering coefficients are based on Mie
   theory.

Geometry
   FDS approximates the governing equations on a rectilinear mesh.
   Rectangular obstructions are forced to conform with the underlying
   mesh.

Multiple Meshes
   This is a term used to describe the use of more than one rectangular
   mesh in a calculation. It is possible to prescribe more than one
   rectangular mesh to handle cases where the computational domain is
   not easily embedded within a single mesh.

Parallel Processing
   FDS employs OpenMP :raw-latex:`\cite{Chapman:OpenMP}`, a programming
   interface that exploits multiple processing units on a single
   computer. For clusters of computers, FDS employs Message Passing
   Interface (MPI) :raw-latex:`\cite{Gropp:1}`. Details can be found in
   Sec. `[info:parallelprocessing] <#info:parallelprocessing>`__.

Boundary Conditions
   All solid surfaces are assigned thermal boundary conditions, plus
   information about the burning behavior of the material. Heat and mass
   transfer to and from solid surfaces is usually handled with empirical
   correlations, although it is possible to compute directly the heat
   and mass transfer when performing a Direct Numerical Simulation
   (DNS).

What’s New in FDS 6?
====================

Many of the changes in FDS 6 are improvements to the various sub-models
that do not affect the basic structure or parameters of the input file.
Most of the changes listed below do not require additional input
parameters beyond those used in FDS 5.

**Hydrodynamics and Turbulence**

-  Conservative, total variation diminishing (TVD) scalar transport is
   implemented: Superbee (VLES default) and CHARM (LES and DNS default).
   These schemes prevent over-shoots and under-shoots in species
   concentrations and temperature.


-  Improved models for the turbulent viscosity are implemented:
   Deardorff (default), Dynamic Smagorinsky, and Vreman. These models
   provide more dynamic range to the flow field for coarse resolution
   and converge to the correct solution at fine resolution.

-  The conservative form of the sensible enthalpy equation is satisfied
   by construction in the FDS 6 formulation, eliminating temperature
   anomalies and energy conservation errors due to numerical mixing.

-  The baroclinic torque is included by default.

-  Improvements are made to the wall functions for momentum and heat
   flux. An optional wall heat flux model accounts for variable Prandtl
   number fluids.

-  Jarrin’s Synthetic Eddy Method (SEM) is implemented for turbulent
   boundary conditions at vents.

**Species and Combustion**

-  Custom species mixtures (“lumped species”) can be defined with the
   input group SPEC.

-  Turbulent combustion is handled with a new partially-stirred batch
   reactor model. At the subgrid level, species exist in one of two
   states: unmixed or mixed. The degree of mixing evolves over the FDS
   time step by the interaction by exchange with the mean (IEM) mixing
   model. Chemical kinetics may be considered infinitely fast or obey an
   Arrhenius rate law.

-  It is now possible to transport, produce, and consume product species
   such as CO and soot. Chemical mechanisms must be provided by the user
   and may include reversible reactions.

-  It is now possible to deposit aerosol species onto surfaces.

-  There are an increased number of predefined species that now include
   liquid properties.

**Lagrangian Particles**

-  The functionality of Lagrangian particles has expanded to include the
   same heat transfer and pyrolysis models that apply to solid walls. In
   other words, you can now assign a set of surface properties to
   planar, cylindrical, or spherical particles much like you would for a
   solid surface.

-  More alternatives and user-defined option are available for the
   liquid droplet size distribution.

-  You can specify the radiative properties of the liquid droplets.

-  Drag effects of thin porous media (i.e., window screens) can be
   simulated using planes of particles.

**Solid Phase Heat Transfer and Pyrolysis**

-  The basic 1-D heat transfer and pyrolysis model for solid surfaces
   remains the same, but there has been a change in several of the input
   parameters to expand functionality and readability of the input file.

-  The pyrolysis model allows for the surface to shrink or swell, based
   on the specified material densities.

**HVAC**

-  Filters, louvered vents, and heating/cooling capability has been
   added for HVAC systems.

-  HVAC is now functional with MPI.

**Radiation**

-  RadCal database has been extended to include additional fuel species.

-  In cells with heat release, the emission term is based on a corrected
   :math:`\sigma \, T^4` such that when this term is integrated over the
   flame volume the specified radiative fraction (default 0.35) is
   recovered. This differs from FDS 5 and earlier where the radiative
   fraction times the heat release rate was applied locally as the
   emission term.

**Multi-Mesh Computations**

-  By default, FDS now iterates pressure and velocity at mesh and solid
   boundaries. You can control the error tolerance and maximum number of
   iterations via parameters on the PRES line.

**Control Functions**

-  CTRL functions have been extended to include math operations.

-  The evaluation of RAMPs and DEVCs can be stopped, freezing their
   value, based upon the activation of a device or control function.

**Devices and Output**

-  Multiple pipe networks can be specified for sprinklers for reduction
   of flow rate based on the number of operating heads.

-  The numerical value of a control function can be output with a DEVC.

-  A line of devices can be specified using a number of POINTS on one
   DEVC line.

-  Statistical outputs for RMS, covariance, and correlation coefficient
   are available.

.. [1]
   The Mach Number, Ma, is the ratio of the flow speed over the speed of
   sound.
