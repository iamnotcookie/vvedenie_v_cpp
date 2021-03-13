cmake_minimum_required(VERSION 3.0)

set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/bin)
set(LIBRARY_OUTPUT_DIR ${CMAKE_SOURCE_DIR}/lib)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR})

project(MyProject C CXX)
add_custom_command(
	OUTPUT A/index.h
	COMMAND python3 ${PROJECT_SOURCE_DIR}/A/preparing.py A/index.h
	DEPENDS A/preparing.py
	COMMENT "prepared" 
)
set(MAIN_SOURCE C/main.cpp C/main.h)

add_custom_target(RunGenerator DEPENDS index.h COMMENT " ")
include_directories(B)
include_directories(${PROJECT_SOURCE_DIR})


add_executable(MyProject ${MAIN_SOURCE})
add_dependencies(MyProject RunGenerator)
add_subdirectory(B)
target_link_libraries(MyProject MyLibrary)
