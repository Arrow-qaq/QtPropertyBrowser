
cmake_minimum_required(VERSION 3.22)

PROJECT(QtPropertyBrowser)

OPTION(QtPropertyBrowser_BUILD_EXAMPLES "Build examples" ON)
OPTION(QtPropertyBrowser_BUILD_STATIC "Build static" ON)
OPTION(QtPropertyBrowser_BUILD_SHARE "Build share" OFF)

#-----------------------------------------------------------------------------
# Output directories.
#
SET(output_dir ${QtPropertyBrowser_BINARY_DIR}/bin)
FOREACH(type LIBRARY RUNTIME ARCHIVE)
  IF(NOT DEFINED CMAKE_${type}_OUTPUT_DIRECTORY)
    SET(CMAKE_${type}_OUTPUT_DIRECTORY ${output_dir} CACHE INTERNAL "Single output directory for building all libraries.")
  ENDIF()
ENDFOREACH()

#-----------------------------------------------------------------------------
# Qt
#
set(CMAKE_PREFIX_PATH $ENV{QTDIR512})
find_package(Qt5 COMPONENTS Core Widgets Gui REQUIRED )

include_directories(
  ${Qt5Core_INCLUDE_DIRS}
  ${Qt5Widgets_INCLUDE_DIRS}
  ${Qt5Gui_INCLUDE_DIRS}
  )

set(QT_LIBRARIES 
  Qt5::Core 
  Qt5::Widgets 
  Qt5::Gui 
)

#-----------------------------------------------------------------------------
# Subdirectories
#
ADD_SUBDIRECTORY(src)
IF(QtPropertyBrowser_BUILD_EXAMPLES)
  ADD_SUBDIRECTORY(examples)
ENDIF()

#-----------------------------------------------------------------------------
# Generate QtPropertyBrowserConfig file
#
CONFIGURE_FILE(UseQtPropertyBrowser.cmake.in
               ${QtPropertyBrowser_BINARY_DIR}/UseQtPropertyBrowser.cmake COPYONLY)

INCLUDE(GenerateQtPropertyBrowserConfig.cmake)
