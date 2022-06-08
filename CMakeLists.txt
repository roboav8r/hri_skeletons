cmake_minimum_required(VERSION 3.5)
project(hri_skeletons)

# Default to C99
if(NOT CMAKE_C_STANDARD)
  set(CMAKE_C_STANDARD 99)
endif()

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# find dependencies
find_package(ament_cmake REQUIRED)
find_package(ament_cmake_python REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rclpy REQUIRED)
find_package(sensor_msgs REQUIRED)
#find_package(hri_mgs REQUIRED)
find_package(cv_bridge REQUIRED)

# Add subdirectory containing pose_extractor C++ package & headers
add_subdirectory(hri_skeletons/pose_extractor)

# Install Python module
ament_python_install_package(${PROJECT_NAME})

# Install Python executables
install(PROGRAMS
  hri_skeletons/run
  hri_skeletons/urdf_generator.py
  hri_skeletons/jointstate.py
  urdf/human-tpl.xacro
  DESTINATION lib/${PROJECT_NAME}
)
install(PROGRAMS
  hri_skeletons/modules/inference_engine.py
  hri_skeletons/modules/input_reader.py
  hri_skeletons/modules/draw.py
  hri_skeletons/modules/parse_poses.py
  hri_skeletons/modules/pose.py
  hri_skeletons/modules/one_euro_filter.py   
  DESTINATION lib/${PROJECT_NAME}/modules
)

if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # the following line skips the linter which checks for copyrights
  # uncomment the line when a copyright and license is not present in all source files
  #set(ament_cmake_copyright_FOUND TRUE)
  # the following line skips cpplint (only works in a git repo)
  # uncomment the line when this package is not in a git repo
  #set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()
