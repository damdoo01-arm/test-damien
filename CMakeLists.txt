cmake_minimum_required(VERSION 3.18)
project(kleidiai_link_test CXX)

add_library(kleidiai_mlas STATIC
  sgemm_kleidiai.cpp
)

target_include_directories(kleidiai_mlas PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/kleidiai/include)

add_executable(test_runner main.cpp)
target_link_libraries(test_runner PRIVATE kleidiai_mlas)