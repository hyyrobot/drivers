cmake_minimum_required(VERSION 2.8.3)
project(hokuyo)

find_package(autoware_build_flags REQUIRED)
find_package(catkin REQUIRED COMPONENTS
  roscpp
  sensor_msgs
)
find_package(Boost 1.53 REQUIRED system serialization)

catkin_package()

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")
include_directories(${catkin_INCLUDE_DIRS} ${Boost_INCLUDE_DIRS})

add_executable(hokuyo_3d nodes/hokuyo_3d/hokuyo_3d.cpp nodes/hokuyo_3d/vssp.hpp)
target_link_libraries(hokuyo_3d ${catkin_LIBRARIES} ${Boost_LIBRARIES})

install(TARGETS hokuyo_3d
  ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
  RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

install(DIRECTORY scripts/
  DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/launch
  PATTERN ".svn" EXCLUDE
)
