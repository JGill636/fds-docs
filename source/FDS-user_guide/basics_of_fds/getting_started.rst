.. _label_getting_started:

***************
Getting Started
***************

.. role:: raw-latex(raw)
   :format: latex
..

FDS is a computer program that solves equations that describe the
evolution of fire. It is a Fortran program that reads input parameters
from a text file, computes a numerical solution to the governing
equations, and writes user-specified output data to files. Smokeview is
a companion program that reads FDS output files and produces animations
on the computer screen. Smokeview has a simple menu-driven interface.
FDS does not. However, there are various third-party programs that have
been developed to generate the text file containing the input parameters
needed by FDS.

This guide describes how to obtain FDS and Smokeview and how to use FDS.
A separate document :raw-latex:`\cite{Smokeview_Users_Guide}` describes
how to use Smokeview.

.. _`info:acquire`:

How to Acquire FDS and Smokeview
================================

Detailed instructions on how to download executables, manuals,
source-code and related utilities, can be found at the project home
page:

.. container:: center

   https://pages.nist.gov/fds-smv/

The typical FDS/Smokeview distribution consists of an installation
package or compressed archive, which is available for MS Windows,
Mac OS X, and Linux.

If you ever want to keep an older version of FDS and Smokeview, copy the
installation directory to some other place so that it is not overwritten
during the updated installation.

Computer Hardware Requirements
==============================

The only hard requirement to run the compiled versions of FDS and
Smokeview is a 64 bit Windows, Linux, or Mac OS X operating system. The
single computer or compute cluster ought to have fast processors (CPUs),
and at least 2 to 4 GB RAM per core. The CPU speed will determine how
long the computation will take to finish, while the amount of RAM will
determine how many mesh cells can be held in memory. A large hard drive
is required to store the output of the calculations. It is not unusual
for the output of a single calculation to consume more than 10 GB of
storage space.

Most computers purchased within the past few years are adequate for
running Smokeview with the caveat that additional memory (RAM) should be
purchased to bring the memory size up to at least 2 GB. This is so the
computer can display results without “swapping” to disk. For Smokeview
it is also important to obtain a fast graphics card for the PC used to
display the results of the FDS computations.

Running FDS using MPI requires shared disk access to each computer where
cases will be run. On Windows systems this involves a domain network
with the ability to share folders. On a Linux or Mac OS X system this
involves NFS cross mounted files systems with ssh keys setup for
passwordless login. For Multi-Mesh calculations, the FDS can operate
over standard 100 Mb/s networks. A gigabit (1000 Mb/s) network will
further reduce network communication times improving data transfer rates
between instances of FDS running the parallel cases.

Computer Operating System (OS) and Software Requirements
========================================================

The goal of making FDS and Smokeview publicly available has been to
enable practicing engineers to perform fairly sophisticated simulations
at a reasonable cost. Thus, FDS and Smokeview have been designed for
computers running Microsoft Windows, Mac OS X, and Linux.

**MS Windows**
   An installation package is available for the 64 bit Windows operating
   system. It is not recommended to run FDS/Smokeview under any version
   of MS Windows released prior to Windows 7.

**Mac OS X**
   Pre-compiled executables are installed into a user selected directory
   using an installation script. Mac OS X 10.4.x or better is
   recommended. You can always download the latest version of FDS source
   and compile FDS for other versions of OS X (See
   Appendix `[info:compilation] <#info:compilation>`__ for details).

**Linux**
   Pre-compiled executables are installed into a user selected directory
   using an installation script. If the pre-compiled FDS executable does
   not work (usually because of library incompatibilities), the FDS
   Fortran source code can be downloaded and compiled (See
   Appendix `[info:compilation] <#info:compilation>`__ for details). If
   Smokeview does not work on the Linux workstation, you can use the
   Windows version to view FDS output.

Installation Testing
====================

If you are running FDS under a quality assurance plan that requires
installation testing, a test procedure is provided in Appendix B of the
FDS Verification Guide :raw-latex:`\cite{FDS_Verification_Guide}`. This
guide can be obtained from the FDS-SMV website.
