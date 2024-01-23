cmake_minimum_required(VERSION 3.22)

project(QtPropertyBrowser)

option(QtPropertyBrowser_BUILD_EXAMPLES "Build examples" ON)
option(QtPropertyBrowser_BUILD_STATIC "Build static" ON)
option(QtPropertyBrowser_BUILD_SHARE "Build share" OFF)

# -----------------------------------------------------------------------------
# Output directories.
#
set(output_dir ${QtPropertyBrowser_BINARY_DIR}/bin)
foreach(type LIBRARY RUNTIME ARCHIVE)
  if(NOT DEFINED CMAKE_${type}_OUTPUT_DIRECTORY)
    set(CMAKE_${type}_OUTPUT_DIRECTORY
        ${output_dir}
        CACHE INTERNAL "Single output directory for building all libraries.")
  endif()
endforeach()

# -----------------------------------------------------------------------------
# Qt
#
# 开启自动生成moc|uic|rcc文件
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_PREFIX_PATH ${QT512_DIR})
message("Qt512 DIR:${QT512_DIR}")
find_package(
  Qt5
  COMPONENTS Core Widgets Gui
  REQUIRED)

include_directories(${Qt5Core_INCLUDE_DIRS} ${Qt5Widgets_INCLUDE_DIRS}
                    ${Qt5Gui_INCLUDE_DIRS})

set(QT_LIBRARIES Qt5::Core Qt5::Widgets Qt5::Gui)

# -----------------------------------------------------------------------------
# Subdirectories
#
add_subdirectory(src)
if(QtPropertyBrowser_BUILD_EXAMPLES)
  add_subdirectory(examples)
endif()
