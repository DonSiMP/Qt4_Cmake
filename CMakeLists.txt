## version an project name
cmake_minimum_required(VERSION 2.8.3)
project(pcl_visualizer)

## c++11
set( CMAKE_BUILD_TYPE "Release" )
set( CMAKE_CXX_FLAGS "-std=c++11 -O3 -Wno-deprecated" )

## QT4
find_package( Qt4 REQUIRED )
include( ${QT_USE_FILE})
add_definitions(${QT_DEFINITIONS})

## VTK
find_package( VTK REQUIRED )

## PCL
find_package( PCL REQUIRED COMPONENT common io )
include_directories( "/usr/include/pcl-1.7" )

## eigen3
include_directories( "/usr/include/eigen3" )

set( CMAKE_INCLUDE_CURRENT_DIR ON )

## compile
set( QT_SOURCES_UI pclviewer.ui )
set( QT_SOURCES_HEADER pclviewer.h )
set( QT_SOURCES_CPP main.cpp pclviewer.cpp )

QT4_WRAP_UI(QT_UI_MOC ${QT_SOURCES_UI})
QT4_WRAP_CPP(QT_HEADER_MOC ${QT_SOURCES_HEADER})

add_executable(pcl_visualizer ${QT_UI_MOC} ${QT_SOURCES_CPP} ${QT_SOURCES_HEADER} ${QT_HEADER_MOC} )
target_link_libraries(pcl_visualizer ${PCL_LIBRARIES} ${QT_LIBRARIES} /usr/lib/libQVTK.so.5.8.0 /opt/ros/indigo/lib/libcv_bridge.so -lboost_system -lboost_filesystem -lpcl_common -lpcl_octree -lpcl_io -lpcl_filters -lpcl_segmentation -lpcl_visualization )