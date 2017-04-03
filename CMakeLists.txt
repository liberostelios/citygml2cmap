# Created by the script cgal_create_CMakeLists
# This is the CMake script for compiling a set of CGAL applications.

project( 3d_linking )

cmake_minimum_required(VERSION 2.8.11)

# This is to force the compiler comply with c++11 standard - libcitygml stuff
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -fPIC")

# CGAL and its components
find_package( CGAL QUIET COMPONENTS  )
find_package( OpenGL REQUIRED )

if ( NOT CGAL_FOUND )

  message(STATUS "This project requires the CGAL library, and will not be compiled.")
  return()  

endif()

# include helper file
include( ${CGAL_USE_FILE} )


# Boost and its components
find_package( Boost REQUIRED )

if ( NOT Boost_FOUND )

  message(STATUS "This project requires the Boost library, and will not be compiled.")

  return()  

endif()

# Include libcitygml
INCLUDE_DIRECTORIES( /usr/local/include/citygml )

# Creating entries for all C++ files with "main" routine
# ##########################################################
include( CGAL_CreateSingleSourceCGALProgram )

create_single_source_cgal_program( "main.cpp" )

target_link_libraries( main citygml ${XERCESC_LIBRARY} ${OPENGL_LIBRARIES} )