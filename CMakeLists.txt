cmake_minimum_required(VERSION 2.8.3)
project(kinematics_toolbox)

## Find catkin macros and libraries
find_package(catkin REQUIRED
  geometry_msgs
)

## System dependencies are found with CMake's conventions
find_package(cmake_modules REQUIRED)
find_package(Eigen3 REQUIRED)
set(Eigen3_INCLUDE_DIRS ${EIGEN3_INCLUDE_DIR})

###################################
## catkin specific configuration ##
###################################

catkin_package(
  INCLUDE_DIRS    include
  LIBRARIES       ${PROJECT_NAME}
                  ${PROJECT_NAME}_ros_types
  CATKIN_DEPENDS  geometry_msgs
  DEPENDS         Eigen3
)

###########
## Build ##
###########

## Specify additional locations of header files
include_directories(include SYSTEM
  ${EIGEN3_INCLUDE_DIR}
  ${catkin_INCLUDE_DIRS}
)

add_definitions("-Wall -Wextra -Wpedantic -Wconversion -Werror -std=c++0x -O3 -g")

#######################
## Build - Libraries ##
#######################

add_library(${PROJECT_NAME}
  include/${PROJECT_NAME}/kinematics.h
  src/kinematics.cpp
)
target_link_libraries(${PROJECT_NAME}
  ${catkin_LIBRARIES}
)

add_library(${PROJECT_NAME}_ros_types
  include/${PROJECT_NAME}/kinematics_ros_types.h
  src/kinematics_ros_types.cpp
)
target_link_libraries(${PROJECT_NAME}_ros_types
  ${catkin_LIBRARIES}
)

#########################
## Build - Executables ##
#########################


#############
## Install ##
#############


#############
## Testing ##
#############
