cmake_minimum_required(VERSION 3.4)
project(hello)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(hello ${CMAKE_CURRENT_SOURCE_DIR}/hello.cpp)
