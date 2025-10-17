cmake_minimum_required(VERSION 3.14)

project(main)

add_subdirectory(.. ${CMAKE_CURRENT_BINARY_DIR}/ccache)

add_executable(main main.cpp)
set_target_properties(main PROPERTIES CXX_STANDARD 17)
