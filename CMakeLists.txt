cmake_minimum_required(VERSION 3.24)

set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/project/ARMCC.cmake)
include(${CMAKE_SOURCE_DIR}/project/Toolchain.cmake)
set_toolchain()

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

project(sdk C CXX)

__compiler_armcc(C)
__compiler_armcc(CXX)

file(GLOB_RECURSE SOURCES sources/*.c sources/*.cpp)

add_library(sdk ${SOURCES})
add_library(crt0 OBJECT sources/crt0/MPCore/crt0.cpp)

target_include_directories(crt0 PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_include_directories(sdk PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
