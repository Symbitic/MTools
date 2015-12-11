################################################################################
# Copyright (c) 2015 Mutant Engine Contributors.
#
# This file is part of MTools.
#
# MTools is free software; you can redistribute it and/or modify it under the
# terms of version 3 of the GNU General Public License, as published by the
# Free Software Foundation.
#
# In addition to the permissions in the GNU General Public License, the authors
# give you unlimited permission to link the compiled version of MTools into
# combinations with other programs, and to distribute those combinations
# without any restriction coming from the use of MTools. The restrictions of the
# GNU General Public License still apply in other respects.
#
# MTools is distributed in the hope that it will be useful, but WITHOUT ANY
# WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR
# A PARTICULAR PURPOSE. See the GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License along with
# MTools. If not, see <http://www.gnu.org/licenses/>.
################################################################################

cmake_minimum_required(VERSION 3.0.0 FATAL_ERROR)
cmake_policy(SET CMP0048 NEW)

include(FeatureSummary)
include(GenerateExportHeader)

project(MTools VERSION 0.0.1)

option(ENABLE_DOC "Build the Sphinx documentation" OFF)

find_package(MCM "0.0.1" CONFIG)
set_package_properties(MCM PROPERTIES
    TYPE REQUIRED
    DESCRIPTION "Mutant CMake Modules"
    URL "https://github.com/Symbitic/MCM"
)

feature_summary(WHAT ALL FATAL_ON_MISSING_REQUIRED_PACKAGES)

if(ENABLE_DOC)
    add_subdirectory(doc)
endif()

mutant_setup_version(${PROJECT_VERSION}
    PACKAGE_VERSION_FILE "MToolsConfigVersion.cmake")

set(CMAKECONFIG_INSTALL_DIR "${MUTANT_INSTALL_CMAKEPACKAGEDIR}/MTools")

mutant_package(MTools
    PACKAGE_FILE "${CMAKE_CURRENT_SOURCE_DIR}/MToolsConfig.cmake.in"
    INSTALL_DESTINATION ${CMAKECONFIG_INSTALL_DIR}
)

install(FILES "${CMAKE_CURRENT_BINARY_DIR}/MCoreConfigVersion.cmake"
    DESTINATION ${CMAKECONFIG_INSTALL_DIR})
