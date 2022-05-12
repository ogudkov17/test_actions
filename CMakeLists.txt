cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project(hello)

add_executable(hello hello.cpp)

option(COVERALLS "Generate coveralls data" OFF)

if (COVERALLS)
		target_compile_options(hello PRIVATE --coverage -fprofile-arcs -ftest-coverage)
		target_link_libraries(hello PRIVATE --coverage -fprofile-arcs -ftest-coverage)
endif()

option(BUILD_TESTS "Build tests" OFF)

if (BUILD_TESTS)
	enable_testing()
	#file(GLOB ./ tests/*.cpp)
	add_executable(check tests/test.cpp)
	target_compile_options(check PRIVATE --coverage -fprofile-arcs -ftest-coverage)
	#include_directories(gtest/include)
	set_target_properties(check PROPERTIES LINKER_LANGUAGE CXX)
	target_link_libraries(check gtest gtest_main pthread --coverage -fprofile-arcs -ftest-coverage)
	#add_test(NAME check COMMAND check)

	include(GoogleTest)

	gtest_discover_tests(check)
endif()


