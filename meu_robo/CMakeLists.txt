cmake_minimum_required(VERSION 3.8)
project(meu_robo)

# Ensure you are using the correct C++ compiler options
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wall -Wextra -Wpedantic)
endif()

# Find dependencies
find_package(ament_cmake REQUIRED)
find_package(rclcpp REQUIRED)
find_package(gazebo_ros_pkgs REQUIRED)
find_package(ros_gz_sim REQUIRED)
find_package(geometry_msgs REQUIRED)
find_package(sensor_msgs REQUIRED)

# Set up Gazebo model directory for SDF files
set(MODEL_PATH "/home/laelt/ros2_ws/src/meu_robo/models")

# Ensure the path to Gazebo models is included in CMake
file(GLOB MODEL_FILES "${MODEL_PATH}/*.sdf")

# Optional: If you have custom Gazebo plugins, find them
# find_package(gazebo REQUIRED) # If you're writing your own plugins, this may be necessary

# Install launch files
install(DIRECTORY launch/
  DESTINATION share/${PROJECT_NAME}/launch
)

install(DIRECTORY ${MODEL_PATH}/
  DESTINATION share/${PROJECT_NAME}/models
)

# Testing section (optional, for unit testing)
if(BUILD_TESTING)
  find_package(ament_lint_auto REQUIRED)
  # Skipping linters for now
  set(ament_cmake_copyright_FOUND TRUE)
  set(ament_cmake_cpplint_FOUND TRUE)
  ament_lint_auto_find_test_dependencies()
endif()

ament_package()

