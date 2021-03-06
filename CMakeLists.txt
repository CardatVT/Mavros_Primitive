cmake_minimum_required(VERSION 2.8.3)
project(mavros_primitive)

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
  cv_bridge
  image_transport
  libuvc_camera
  mavros
  roscpp
  sensor_msgs
  std_msgs
  
)
#must be seperate
find_package( OpenCV REQUIRED )

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if you package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need
catkin_package(
  INCLUDE_DIRS include
  LIBRARIES mavros_primitive
  CATKIN_DEPENDS cv_bridge image_transport libuvc_camera  roscpp sensor_msgs std_msgs #mavlink OpenCV
  DEPENDS system_lib
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)
include_directories(
   src/ 
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
)

## Declare a cpp library
 #add_library(obstacle_avoidance
 #  src/${PROJECT_NAME}/obstacle_avoidance.cpp
 #)

## Declare a cpp executable
add_executable(mavros_primitive_node 
src/mavros_primitive.cpp
)

## Add cmake target dependencies of the executable/library
## as an example, message headers may need to be generated before nodes
# add_dependencies(obstacle_avoidance_node obstacle_avoidance_generate_messages_cpp)

## Specify libraries to link a library or executable target against
 target_link_libraries(mavros_primitive_node
   ${OpenCV_LIBRARIES}
   ${catkin_LIBRARIES}
 )



