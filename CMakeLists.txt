cmake_minimum_required(VERSION 2.4)

project(YAQ CXX C)

message(status ${CMAKE_INCLUDE_PATH})

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2 -Wall -Wfatal-errors")


if(PROJECT_BINARY_DIR STREQUAL PROJECT_SOURCE_DIR)
   message(FATAL_ERROR "In-tree build attempt detected, aborting. Set your build dir outside your source dir, delete CMakeCache.txt from source root and try again.")
endif()

if (("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang") OR CMAKE_COMPILER_IS_GNUCXX)
    include(CheckCXXCompilerFlag)
    check_cxx_compiler_flag(-std=c++11 SUPPORTS_STD_CXX11)
    check_cxx_compiler_flag(-std=c++0x SUPPORTS_STD_CXX01)
    if(SUPPORTS_STD_CXX11)
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
        set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c++11")
    elseif(SUPPORTS_STD_CXX01)
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
        set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c++0x")
    else()
        message(ERROR "Compiler does not support -std=c++11 or -std=c++0x.")
    endif()
endif()


set(${PROJECT_NAME}_INCLUDE_DIRS ${PROJECT_SOURCE_DIR}/include
    CACHE INTERNAL "${PROJECT_NAME}: Include Directories" FORCE)




include_directories(include)

add_executable("${PROJECT_NAME}example1" examples/example1.cpp)
