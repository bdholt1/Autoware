cmake_minimum_required(VERSION 2.8.3)
project(lidar_kf_track)


find_package(catkin REQUIRED COMPONENTS
  pcl_ros
  roscpp
  std_msgs
  autoware_msgs
  tf
  jsk_recognition_msgs
  jsk_rviz_plugins
  lidar_euclidean_cluster_detect
  )

find_package(OpenCV REQUIRED)

set(CMAKE_CXX_FLAGS "-std=c++11 -O2 -Wall ${CMAKE_CXX_FLAGS}")

catkin_package(
  CATKIN_DEPENDS
  pcl_ros
  roscpp
  std_msgs
  autoware_msgs
  tf
  jsk_recognition_msgs
  jsk_rviz_plugins
  lidar_euclidean_cluster_detect
)

include_directories(
  ${catkin_INCLUDE_DIRS}
  ${OpenCV_INCLUDE_DIRS}
  include
  )
link_directories(${PCL_LIBRARY_DIRS})
link_directories(${OpenCV_LIBRARY_DIRS})

#KalmanFilter Track

add_executable(lidar_kf_track
  nodes/lidar_kf_track/lidar_kf_track_core.cpp
  nodes/lidar_kf_track/lidar_kf_track.cpp
  nodes/lidar_kf_track/hungarian_alg.cpp
  nodes/lidar_kf_track/kalman.cpp
  )
target_link_libraries(lidar_kf_track
  ${catkin_LIBRARIES}
  ${PCL_LIBRARIES}
  )
add_dependencies(lidar_kf_track
  ${catkin_EXPORTED_TARGETS}
  )