========
 MTools 
========

|Status| |Release| |License|

MTools provides several tools to help automate (and enhance) Mutant Engine.

.. contents::
   :local:
   :depth: 1
   :backlinks: none

About
-----

MTools was created to help automate as many tasks in Mutant Engine as possible.
It handles meta-code creation, inserts runtime error-checks, and many other
advanced features.

For more information about MTools, see
https://symbitic.github.com/mtools/

Getting Started
---------------

Mutant Engine is still in pre-release beta. Users must clone the GitHub
repository and build it themselves if they wish to use MTools. In the future,
binary releases may be uploaded for easier use.

Building
--------

Mutant Engine projects uses `CMake`_ as the build system.
CMake 3.0.0 or later is required.

The recommended way of building MTools is by building the entire Mutant Engine
toolchain. To download and build Mutant Engine using CMake and `Ninja`_
(Recommended), run:

.. code-block:: console

   $ git clone https://github.com/Symbitic/Mutant
   $ mkdir Mutant/build
   $ cd Mutant/build
   $ cmake -G "Ninja" ..
   $ ninja

CMake will then handle downloading, configuring, building, and packaging of
all Mutant Engine components. An active internet connection is needed to
download the Mutant Engine sub-components.

Legal
-----

MTools is distributed under the terms of version 3 of the
`GNU General Public License`_, with a linking exception. For full terms, see
`COPYING.txt`_.

.. |Status| image:: https://img.shields.io/travis/Symbitic/MTools.svg?style=flat-square&label=Build
   :alt: TravisCI status.
   :target: https://travis-ci.org/Symbitic/MTools

.. |Release| image:: https://img.shields.io/github/release/Symbitic/MTools.svg?style=flat-square&label=Release
   :alt: Latest release of MTools.
   :target: https://github.com/Symbitic/MTools/releases/latest

.. |License| image:: https://img.shields.io/github/license/Symbitic/MTools.svg?style=flat-square&label=License
   :alt: GNU GPL v3.0
   :target: http://choosealicense.com/licenses/gpl-3.0/

.. _CMake: http://www.cmake.org/

.. _Ninja: http://martine.github.io/ninja/

.. _GNU General Public License: http://www.gnu.org/licenses/gpl-3.0.html

.. _COPYING.txt: ./COPYING.txt: 
