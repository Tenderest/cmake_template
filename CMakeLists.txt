cmake_minimum_required(VERSION 3.25)
project(demo)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_C_STANDARD 99)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# set execuable output path
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin)
# set library output path
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin)
# set library path
set(CMAKE_LIBRARY_PATH ${CMAKE_CURRENT_SOURCE_DIR}/bin)
# set(CMAKE_BUILD_TYPE Debug)
set(CMAKE_BUILD_TYPE Release)
# Control whether to call the output directory function echo_dir

# use this in sub directory
set(ALL_LIBS "")
set(ALL_INCS "")

add_subdirectory(inc)

add_subdirectory(lib)

add_subdirectory(src)
