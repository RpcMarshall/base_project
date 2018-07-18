cmake_minimum_required(VERSION 2.8.3)
project(mypkg)

find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  roscpp
  rospy
  std_msgs
  message_generation
  gazebo_ros
)

find_package(gazebo REQUIRED)

add_service_files(
  FILES
  AddTwoInts.srv
)

generate_messages(
  DEPENDENCIES
    std_msgs
)

catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES my_pkg0
#  CATKIN_DEPENDS roscpp rospy std_msgs
#  DEPENDS system_lib
  DEPENDS
    roscpp
    gazebo_ros
)

link_directories(${GAZEBO_LIBRARY_DIRS})
include_directories(
# include
  ${Boost-INCLUDE_DIR}
  ${catkin_INCLUDE_DIRS}
  ${GAZEBO_INCLUDE_DIRS}
)

add_library(${PROJECT_NAME} src/simple_world_plugin.cpp)
target_link_libraries(${PROJECT_NAME} ${catkin_LIBRARIES} ${GAZEBO_LIBRARIES})

add_executable(hello src/hello.cpp)
add_executable(pubvel src/pubvel.cpp)
add_executable(subvel src/subvel.cpp)
add_executable(reverse_teleop src/reverse_teleop.cpp)
add_executable(set_color src/set_bg_color.cpp)
add_executable(add_two_ints_server src/add_two_ints_server.cpp)
add_executable(add_two_ints_client src/add_two_ints_client.cpp)
add_executable(test_output src/test_output.cpp)

target_link_libraries(hello ${catkin_LIBRARIES})
target_link_libraries(pubvel ${catkin_LIBRARIES})
target_link_libraries(subvel ${catkin_LIBRARIES})
target_link_libraries(reverse_teleop ${catkin_LIBRARIES})
target_link_libraries(set_color ${catkin_LIBRARIES})
target_link_libraries(add_two_ints_server ${catkin_LIBRARIES})
target_link_libraries(add_two_ints_client ${catkin_LIBRARIES})
target_link_libraries(test_output ${catkin_LIBRARIES})

add_dependencies(add_two_ints_server mypkg_gencpp)
add_dependencies(add_two_ints_client mypkg_gencpp)

