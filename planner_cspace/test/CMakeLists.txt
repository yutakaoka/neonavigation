cmake_minimum_required(VERSION 2.8.3)

find_package(catkin REQUIRED COMPONENTS roscpp rostest nav_msgs tf)

catkin_add_gtest(test_cyclic_vec src/test_cyclic_vec.cpp)
target_link_libraries(test_cyclic_vec ${catkin_LIBRARIES} ${Boost_LIBRARIES})

catkin_add_gtest(test_blockmem_gridmap src/test_blockmem_gridmap.cpp)
target_link_libraries(test_blockmem_gridmap ${catkin_LIBRARIES} ${Boost_LIBRARIES})

catkin_add_gtest(test_blockmem_gridmap_performance src/test_blockmem_gridmap_performance.cpp)
target_link_libraries(test_blockmem_gridmap_performance ${catkin_LIBRARIES} ${Boost_LIBRARIES})
# Force release build since it contains performance test.
set_target_properties(test_blockmem_gridmap_performance PROPERTIES COMPILE_FLAGS "${CMAKE_CXX_FLAGS_RELEASE}")

add_rostest_gtest(test_navigate
  test/navigation_rostest.test
  src/test_navigate.cpp
)
target_link_libraries(test_navigate ${catkin_LIBRARIES})
add_dependencies(test_navigate planner_3d)
