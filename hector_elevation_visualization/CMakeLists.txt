# Catkin User Guide: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/user_guide.html
# Catkin CMake Standard: http://www.ros.org/doc/groovy/api/catkin/html/user_guide/standards.html
cmake_minimum_required(VERSION 2.8.3)
project(hector_elevation_visualization)
# Load catkin and all dependencies required for this package
# TODO: remove all from COMPONENTS that are not catkin packages.
find_package(catkin REQUIRED COMPONENTS visualization_msgs hector_elevation_msgs tf hector_map_tools dynamic_reconfigure cmake_modules)

find_package(Eigen REQUIRED)
include_directories(${EIGEN_INCLUDE_DIRS})
add_definitions(${EIGEN_DEFINITIONS})


# include_directories(include ${Boost_INCLUDE_DIR} ${catkin_INCLUDE_DIRS})
# CATKIN_MIGRATION: removed during catkin migration
# cmake_minimum_required(VERSION 2.4.6)

# CATKIN_MIGRATION: removed during catkin migration
# include($ENV{ROS_ROOT}/core/rosbuild/rosbuild.cmake)

# Set the build type.  Options are:
#  Coverage       : w/ debug symbols, w/o optimization, w/ code-coverage
#  Debug          : w/ debug symbols, w/o optimization
#  Release        : w/o debug symbols, w/ optimization
#  RelWithDebInfo : w/ debug symbols, w/ optimization
#  MinSizeRel     : w/o debug symbols, w/ optimization, stripped binaries
#set(ROS_BUILD_TYPE Debug)


# CATKIN_MIGRATION: removed during catkin migration
# rosbuild_init()

#set the default path for built executables to the "bin" directory
set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)
#set the default path for built libraries to the "lib" directory
set(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)

#uncomment if you have defined messages
#add_message_files(
#  FILES
  # TODO: List your msg files here
#)
#uncomment if you have defined services
#add_service_files(
#  FILES
  # TODO: List your msg files here
#)

generate_dynamic_reconfigure_options(
  cfg/ElevationVisualization.cfg
)

#find Eigen
find_package(cmake_modules)
find_package(Eigen REQUIRED)
include_directories(${EIGEN_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS} cfg/cpp)
add_executable(hector_elevation_visualization src/hector_elevation_visualization_node.cpp src/hector_elevation_visualization.cpp src/hector_elevation_visualization.h)
target_link_libraries(hector_elevation_visualization ${catkin_LIBRARIES})
add_dependencies(hector_elevation_visualization ${PROJECT_NAME}_gencfg)


#add dynamic reconfigure api
#rosbuild_find_ros_package(dynamic_reconfigure)
#include(${dynamic_reconfigure_PACKAGE_PATH}/cmake/cfgbuild.cmake)
#gencfg()

#add_subdirectory(src)
## Generate added messages and services with any dependencies listed here
#generate_messages(
    #TODO DEPENDENCIES geometry_msgs std_msgs
#)

# catkin_package parameters: http://ros.org/doc/groovy/api/catkin/html/dev_guide/generated_cmake_api.html#catkin-package
# TODO: fill in what other packages will need to use this package
catkin_package(
    DEPENDS visualization_msgs hector_elevation_msgs tf hector_map_tools dynamic_reconfigure cmake_modules
    CATKIN_DEPENDS hector_elevation_msgs # TODO
    INCLUDE_DIRS 
    LIBRARIES # TODO
)
