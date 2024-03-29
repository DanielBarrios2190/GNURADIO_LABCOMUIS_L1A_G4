# Copyright 2011,2012,2016,2018,2019 Free Software Foundation, Inc.
#
# This file was generated by gr_modtool, a tool from the GNU Radio framework
# This file is a part of gr-Modulos_L1A
#
# SPDX-License-Identifier: GPL-3.0-or-later
#

########################################################################
# Setup library
########################################################################
include(GrPlatform) #define LIB_SUFFIX

list(APPEND Modulos_L1A_sources
)

set(Modulos_L1A_sources "${Modulos_L1A_sources}" PARENT_SCOPE)
if(NOT Modulos_L1A_sources)
    MESSAGE(STATUS "No C++ sources... skipping lib/")
    return()
endif(NOT Modulos_L1A_sources)

add_library(gnuradio-Modulos_L1A SHARED ${Modulos_L1A_sources})
target_link_libraries(gnuradio-Modulos_L1A gnuradio::gnuradio-runtime)
target_include_directories(gnuradio-Modulos_L1A
    PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../include>
    PUBLIC $<INSTALL_INTERFACE:include>
  )
set_target_properties(gnuradio-Modulos_L1A PROPERTIES DEFINE_SYMBOL "gnuradio_Modulos_L1A_EXPORTS")

if(APPLE)
    set_target_properties(gnuradio-Modulos_L1A PROPERTIES
        INSTALL_NAME_DIR "${CMAKE_INSTALL_PREFIX}/lib"
    )
endif(APPLE)

########################################################################
# Install built library files
########################################################################
include(GrMiscUtils)
GR_LIBRARY_FOO(gnuradio-Modulos_L1A)

########################################################################
# Print summary
########################################################################
message(STATUS "Using install prefix: ${CMAKE_INSTALL_PREFIX}")
message(STATUS "Building for version: ${VERSION} / ${LIBVER}")

########################################################################
# Build and register unit test
########################################################################
include(GrTest)

# If your unit tests require special include paths, add them here
#include_directories()
# List all files that contain Boost.UTF unit tests here
list(APPEND test_Modulos_L1A_sources
)
# Anything we need to link to for the unit tests go here
list(APPEND GR_TEST_TARGET_DEPS gnuradio-Modulos_L1A)

if(NOT test_Modulos_L1A_sources)
    MESSAGE(STATUS "No C++ unit tests... skipping")
    return()
endif(NOT test_Modulos_L1A_sources)

foreach(qa_file ${test_Modulos_L1A_sources})
    GR_ADD_CPP_TEST("Modulos_L1A_${qa_file}"
        ${CMAKE_CURRENT_SOURCE_DIR}/${qa_file}
    )
endforeach(qa_file)
