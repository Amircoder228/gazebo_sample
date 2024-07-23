cmake_minimum_required(VERSION 3.0.2)
project(offb_node)

# Find catkin and any catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  geometry_msgs
  mavros_msgs
)

# Include mavros_msgs directory if built from source
set(CMAKE_PREFIX_PATH "${CMAKE_PREFIX_PATH};${CATKIN_DEVEL_PREFIX}/share/mavros_msgs/cmake")

# Declare a catkin package
catkin_package(
  CATKIN_DEPENDS roscpp geometry_msgs mavros_msgs
)

# Specify additional locations of header files
include_directories(
  ${catkin_INCLUDE_DIRS}
)

# Declare the executable, along with its source files
add_executable(${PROJECT_NAME}_node src/offb_node.cpp)

# Specify libraries to link executable targets against
target_link_libraries(${PROJECT_NAME}_node
  ${catkin_LIBRARIES}
)

