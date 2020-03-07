cmake_minimum_required(VERSION 2.8)
project(tiv)

set(EXECUTABLE_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/bin)

# set some options
# https://cmake.org/cmake/help/latest/prop_tgt/CXX_STANDARD.html
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_C_FLAGS_RELEASE "${CMAKE_C_FLAGS_RELEASE} -Wall -Wextra 
    -O2 -fpermissive -Wall -fexceptions -Wno-unused-result")

set(CMAKE_BUILD_TYPE Release)

set(SRC ${PROJECT_SOURCE_DIR}/src)

set(EXECUTABLE_OUTPUT_PATH bin)

# find files
file(GLOB_RECURSE source_files ${SRC}/*)

add_executable(tiv ${source_files})

install(TARGETS tiv RUNTIME DESTINATION bin)

# libs
target_link_libraries(tiv stdc++fs)

# how to set CXX
# https://gitlab.kitware.com/cmake/community/-/wikis/FAQ
# cmake -DCMAKE_CXX_COMPILER=<path to cpp compier>
