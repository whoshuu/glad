cmake_minimum_required(VERSION 3.10)
cmake_policy(SET CMP0048 NEW)

set(CMAKE_C_COMPILER_NAMES clang gcc)
set(CMAKE_CXX_COMPILER_NAMES clang++ g++)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

project("glad" VERSION 0.1.0 LANGUAGES C CXX)

set(CMAKE_CXX_FLAGS "-Wall -Wextra -Werror -g -mavx2")
set(CMAKE_CXX_FLAGS_DEBUG "-O0")
set(CMAKE_CXX_FLAGS_RELEASE "-O3")

if(CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-deprecated-register")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-address-of-packed-member")
endif()

add_library(glad ${CMAKE_SOURCE_DIR}/glad/glad.c)
target_include_directories(glad PRIVATE ${CMAKE_SOURCE_DIR}/include)
install(TARGETS glad)
install(DIRECTORY ${CMAKE_SOURCE_DIR}/include/ DESTINATION include)
