cmake_minimum_required(VERSION 2.8.3)
project(hello_world)

find_package(catkin REQUIRED COMPONENTS
  roscpp
)

catkin_package()

include_directories(${catkin_INCLUDE_DIRS})

add_executable(hello src/hello.cpp)
target_link_libraries(hello ${catkin_LIBRARIES})

if(CATKIN_ENABLE_TESTING)
  find_package(rostest)
  add_subdirectory(test)
endif()

install(TARGETS ${PROJECT_NAME}
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

