cmake_minimum_required(VERSION 2.8.3)

project(ros2_parameter_server)

if(NOT WIN32)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall -Wextra")
endif()

find_package(ament_cmake REQUIRED)

find_package(builtin_interfaces REQUIRED)
find_package(rclcpp REQUIRED)
find_package(rmw REQUIRED)
find_package(rmw_implementation_cmake REQUIRED)


macro(targets)
	if(NOT "${target_suffix} " STREQUAL " ")
	  get_rclcpp_information("${rmw_implementation}" "rclcpp${target_suffix}")
	endif()
	
	include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src)
        MESSAGE(rclcpp${target_suffix})
	add_executable(ros2_parameter_server${target_suffix} src/main.cpp)
	ament_target_dependencies(ros2_parameter_server${target_suffix}
                "rclcpp${target_suffix}"
		"std_msgs"
	)
   
	install(TARGETS ros2_parameter_server${target_suffix}
                DESTINATION bin)

endmacro()



call_for_each_rmw_implementation(targets GENERATE_DEFAULT)

ament_package()
