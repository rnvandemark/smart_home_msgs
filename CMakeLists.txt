cmake_minimum_required(VERSION 3.5)

project(smart_home_msgs)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
	set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
	add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(catkin REQUIRED COMPONENTS message_generation)
find_package(std_msgs REQUIRED)
find_package(smart_home_interfaces REQUIRED)

# Set a variable for the share directory to look for the message files in
set(smart_home_interfaces_MSGS_DIR
	"${smart_home_interfaces_DIR}/../msg"
)

# Glob all files ending in .msg in the directory
file(GLOB smart_home_interfaces_MSG_PATHS
	"${smart_home_interfaces_MSGS_DIR}/*.msg"
)

# Glob gets the files' full paths, strip all but the file name
foreach(_msg_path ${smart_home_interfaces_MSG_PATHS})
	get_filename_component(_msg_filename "${_msg_path}" NAME)
	list(APPEND smart_home_interfaces_MSG_FILENAMES "${_msg_filename}")
endforeach()

# Specify the original directory and expand the list of message filenames
add_message_files(
	DIRECTORY "${smart_home_interfaces_MSGS_DIR}"
	FILES
	"${smart_home_interfaces_MSG_FILENAMES}"
)

# These messages obviously have the same dependencies as those in smart_home_interfaces
generate_messages(DEPENDENCIES
	std_msgs
)

catkin_package(CATKIN_DEPENDS
	message_runtime
)
