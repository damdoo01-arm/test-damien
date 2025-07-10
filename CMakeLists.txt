cmake_minimum_required(VERSION 3.18)
project(kleidiai_link_test CXX)

add_library(kleidiai_mlas STATIC
  sgemm_kleidiai.cpp
)

# Simulated KleidiAI API reference
target_include_directories(kleidiai_mlas PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/kleidiai/include)

add_executable(test_runner main.cpp)

# 💡 This is where we link the `.lib` explicitly (MSVC only)
if(MSVC)
  set(KLEIDIAI_LIB "${CMAKE_CURRENT_SOURCE_DIR}/kleidiai/lib/kleidiai.lib")
  message(STATUS "Linking to manually specified .lib: ${KLEIDIAI_LIB}")
  target_link_libraries(test_runner PRIVATE "${KLEIDIAI_LIB}")
endif()

target_link_libraries(test_runner PRIVATE kleidiai_mlas)