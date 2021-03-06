cmake_minimum_required(VERSION 2.8.3)
project(goal_sender)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  actionlib
  geometry_msgs
  move_base_msgs
  tf
)

catkin_package(
  CATKIN_DEPENDS roscpp actionlib geometry_msgs move_base_msgs tf
)

# check c++11 / c++0x
include(CheckCXXCompilerFlag)
  CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
  CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
  set(CMAKE_CXX_FLAGS "-std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
  set(CMAKE_CXX_FLAGS "-std=c++0x")
else()
  message(FATAL_ERROR "The compiler ${CMAKE_CXX_COMPILER} has no C++11 support. Please use a different C++ compiler.")
endif()

include_directories(${catkin_INCLUDE_DIRS})

add_executable(goal_sender_node src/goal_sender_node.cpp)
add_dependencies(goal_sender_node ${catkin_EXPORTED_TARGETS})
target_link_libraries(goal_sender_node ${catkin_LIBRARIES})

