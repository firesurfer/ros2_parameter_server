cmake_minimum_required(VERSION 3.5)

project(ros2_parameter_server)

if(NOT WIN32)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Wextra")
endif()

find_package(ament_cmake REQUIRED)

find_package(builtin_interfaces REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rmw REQUIRED)
find_package(rmw_implementation_cmake REQUIRED)



	include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src)

	add_executable(ros2_parameter_server src/main.cpp)
	ament_target_dependencies(ros2_parameter_server
                "rclcpp${target_suffix}"
		"std_msgs"
	)
   
	install(TARGETS ros2_parameter_server
                DESTINATION bin)





ament_package()
