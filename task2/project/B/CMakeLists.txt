cmake_minimum_required(VERSION 3.0)

project(MyLibrary)

set(SOURCE_LIB empty.cpp lib.h)

add_library(MyLibrary SHARED ${SOURCE_LIB})
