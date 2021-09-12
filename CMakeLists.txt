cmake_minimum_required(VERSION 3.14)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -ggdb3 -O0 -Wall -Werror")
set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} -O3 -Wall")

include(FindPkgConfig)
set(CMAKE_FIND_FRAMEWORK LAST)

project(JsonWrapperCpp VERSION 20210912.1)
add_library(JsonWrapperCpp STATIC)
target_sources(JsonWrapperCpp PUBLIC src/swe_json_wrapper.cpp)
