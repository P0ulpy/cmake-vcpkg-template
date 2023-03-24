cmake_minimum_required(VERSION 3.24)
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake)

project(cmake-vcpkg-template)

set(CMAKE_CXX_STANDARD 20)

find_package(SFML COMPONENTS system window graphics CONFIG REQUIRED)
find_package(GLEW REQUIRED)

add_executable(cmake-vcpkg-template main.cpp Shader.cpp Shader.hpp)

target_link_libraries(cmake-vcpkg-template PRIVATE sfml-system sfml-network sfml-graphics sfml-window)
target_link_libraries(cmake-vcpkg-template PRIVATE GLEW::GLEW)
