cmake_minimum_required(VERSION 3.5)

project(smart_home_msgs)

# Default to C++14
if(NOT CMAKE_CXX_STANDARD)
	set(CMAKE_CXX_STANDARD 14)
endif()

if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
	add_compile_options(-Wall -Wextra -Wpedantic)
endif()

find_package(catkin REQUIRED COMPONENTS message_generation std_msgs sensor_msgs)

add_message_files(
	DIRECTORY msg
	FILES
	Color.msg
	ColorPeaksTelem.msg
	CountdownState.msg
	DeviceActivationChange.msg
	Float32Arr.msg
	ModeChange.msg
	ModeChangeRequest.msg
	Point.msg
	WaveParticipantLocation.msg
	WaveUpdate.msg
)

add_service_files(
	DIRECTORY srv
	FILES
	RequestScreenCalibration.srv
	SetScreenCalibrationPointsOfHomography.srv
)

generate_messages(DEPENDENCIES
	std_msgs
	sensor_msgs
)

catkin_package(CATKIN_DEPENDS
	message_runtime
)
