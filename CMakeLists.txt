cmake_minimum_required(VERSION 3.10)
project(hello_world CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)

# Include the header files
include_directories(${PROJECT_SOURCE_DIR}/src)

# Add GoogleTest
include(FetchContent)
FetchContent_Declare(
    googletest
    URL https://github.com/google/googletest/archive/refs/heads/main.zip
    DOWNLOAD_EXTRACT_TIMESTAMP TRUE  
)
FetchContent_MakeAvailable(googletest)



add_library(sample_lib src/function.cpp)

# add_executable(hello_world src/main.cpp)

# target_link_libraries(hello_world sample_lib)

add_executable(sample_test test/sample_test.cpp)

target_link_libraries(sample_test gtest gtest_main sample_lib)

# Enable testing
enable_testing()
add_test(NAME sample_test COMMAND sample_test)