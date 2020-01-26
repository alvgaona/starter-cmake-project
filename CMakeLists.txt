cmake_minimum_required(VERSION 3.11.3)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")

project(start_cmake_project)

# Find packages
find_package(example 1.0 REQUIRED)

# Find all executables
file(GLOB SOURCES src/*.cpp)

# Add GoogleTest library subdirectories
add_subdirectory(thirdparty/googletest)

# Add the testing executable
add_executable(test test/utest_start_cmake_project.cpp)
target_link_libraries(test gtest_main)

# Add the app executable
add_executable(start_cmake_project ${SOURCES})
target_link_libraries(start_cmake_project PRIVATE ${Example_LIBRARIES})
target_include_directories(start_cmake_project PRIVATE include)
target_link_directories(start_cmake_project PRIVATE ${Example_LIBRARY_DIRS})
target_compile_definitions(start_cmake_project PRIVATE ${Example_DEFINITIONS})
