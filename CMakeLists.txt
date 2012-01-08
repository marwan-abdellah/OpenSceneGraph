# Min version of CMake 
cmake_minimum_required (VERSION 2.6)

# Project name 
project (OpenSceneGraph)

# Point to CMake folde to get the Find.cmake file 
set(CMAKE_MODULE_PATH ${CMAKE_SOURCE_DIR}/CMake)
# message (CMAKE_MODULE_PATH-> ${CMAKE_MODULE_PATH})

# Setting OSG path to local version 2.8.3 
set(OSG_DIR /home/abdellah/OpenSceneGraph_2.8.3)

# Set the examples binary directory 
set(BUILD_BIN_DIR "${CMAKE_BINARY_DIR}/Bin")

# OpenSceneGraph Library 
set(OPENSCENEGRAPH_LIBS "")

# Find OSG 
find_package(OSG)
if (OSG_FOUND)
  message("-- Found OSG")
elseif (OSG_FOUND)
  message("-- OSG NOT FOUND")
endif(OSG_FOUND)

# Adding the OSG include directies to my include list  
include_directories(${OSG_INCLUDE_DIR})

# Adding OSG libraries to OPENSCENEGRAPH_LIBS
list(APPEND OPENSCENEGRAPH_LIBS ${OSG_LIBS})

# Find OpenSceneGraph 
find_package(OpenSceneGraph)
if (OpenSceneGraph_FOUND)
  message("-- Found OpenSceneGraph")
elseif (OpenSceneGraph_FOUND)
  message("-- OpenSceneGraph NOT FOUND")
endif(OpenSceneGraph_FOUND)

# Adding the OpenSceneGraph include directies to my include list  
include_directories(${OPENSCENEGRAPH_INCLUDE_DIRS})

# Adding OpenSceneGraph libraries to OPENSCENEGRAPH_LIBS
list(APPEND OPENSCENEGRAPH_LIBS ${OPENSCENEGRAPH_LIBRARIES})

# Find GLUT
find_package(GLUT)
if (GLUT_FOUND)
  message("-- Found GLUT")
elseif (GLUT_FOUND)
  message("-- GLUT NOT FOUND")
endif(GLUT_FOUND)

# Adding the GLUT include directies to my include list  
include_directories(${GLUT_INCLUDE_PATHS})

# Adding GLUT libraries to OPENSCENEGRAPH_LIBS
list(APPEND OPENSCENEGRAPH_LIBS ${GLUT_LIBRARY})

set(BUILD_OSG_EXAMPLES TRUE)

IF (BUILD_OSG_EXAMPLES)
    FIND_PACKAGE(FLTK)
    FIND_PACKAGE(GLUT)
    FIND_PACKAGE(SDL)
    FIND_PACKAGE(FOX)

    SET(wxWidgets_USE_LIBS base core gl net)
    FIND_PACKAGE(wxWidgets)

    # To select a specific version of QT define DESIRED_QT_VERSION
    # via cmake -DDESIRED_QT_VERSION=4
    IF  (DESIRED_QT_VERSION)

        IF  (DESIRED_QT_VERSION MATCHES 4)
          FIND_PACKAGE(Qt4)
        ELSE(DESIRED_QT_VERSION MATCHES 4)
          FIND_PACKAGE(Qt3)
        ENDIF(DESIRED_QT_VERSION MATCHES 4)

    ELSE(DESIRED_QT_VERSION)

        FIND_PACKAGE(Qt4)

        IF  (NOT QT4_FOUND)
            FIND_PACKAGE(Qt3)
        ENDIF(NOT QT4_FOUND)

    ENDIF(DESIRED_QT_VERSION)
    
	# Add the examples subdirectory 
	add_subdirectory(Examples)

ENDIF(BUILD_OSG_EXAMPLES)


# Source Code ".CXX" files 
set(OPENSCENEGRAPH_CORE_SOURCES 
	runOSG.cxx
)
 
add_executable(OpenSceneGraph ${OPENSCENEGRAPH_CORE_SOURCES})
target_link_libraries (OpenSceneGraph ${OPENSCENEGRAPH_LIBS})	



