cmake_minimum_required(VERSION 3.5)

project(cpp2d)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

find_package(LLVM 4.0 REQUIRED CONFIG
    HINTS /usr/local/opt/llvm@4/lib/cmake/)

message(STATUS "Found LLVM ${LLVM_PACKAGE_VERSION}")
message(STATUS "Using LLVMConfig.cmake in: ${LLVM_DIR}")

add_subdirectory(CPP2D)
add_subdirectory(CPP2D_UT_CPP)
