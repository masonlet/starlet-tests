cmake_minimum_required(VERSION 3.23)

set(TEST_NAME starlet_tests)
set(TEST_DIR "${CMAKE_CURRENT_SOURCE_DIR}/tests")

project(${TEST_NAME} LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 20)
set(CMAKE_SUPPRESS_REGENERATION ON)

include(CTest)
enable_testing()

include(FetchContent)
FetchContent_Declare(
  googletest 
  URL https://github.com/google/googletest/archive/refs/tags/v1.17.0.zip 
  DOWNLOAD_EXTRACT_TIMESTAMP TRUE
)
set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

file(GLOB_RECURSE TEST_SOURCES ${TEST_DIR}/*.cpp)
add_executable(${TEST_NAME} ${TEST_SOURCES})

if(NOT BUILD_LOCAL)
  FetchContent_Declare(starlet_math
    GIT_REPOSITORY https://github.com/masonlet/starlet-math.git 
    GIT_TAG main
  )
  FetchContent_Declare(starlet_serializer 
    GIT_REPOSITORY https://github.com/masonlet/starlet-serializer.git 
    GIT_TAG main
  )
  FetchContent_Declare(starlet_scene
    GIT_REPOSITORY https://github.com/masonlet/starlet-scene.git 
    GIT_TAG main
  )
  FetchContent_Declare(starlet_graphics
    GIT_REPOSITORY https://github.com/masonlet/starlet-graphics.git 
    GIT_TAG main
  )
  FetchContent_Declare(starlet_controls
    GIT_REPOSITORY https://github.com/masonlet/starlet-controls.git 
    GIT_TAG main
  )
  FetchContent_Declare(starlet_engine
    GIT_REPOSITORY https://github.com/masonlet/starlet-engine.git 
    GIT_TAG main
  )
  FetchContent_Declare(starlet_logger
    GIT_REPOSITORY https://github.com/masonlet/starlet-logger.git 
    GIT_TAG main
  )
endif()

target_link_libraries(${TEST_NAME} 
  PRIVATE
    gtest_main 
    starlet_math
    starlet_logger
    starlet_serializer
    starlet_scene
    starlet_graphics
    starlet_controls
    starlet_engine
)

include(GoogleTest)
gtest_discover_tests(${TEST_NAME})

set_property(TARGET gtest PROPERTY FOLDER "Tests")
set_property(TARGET gmock PROPERTY FOLDER "Tests")
set_property(TARGET gmock_main PROPERTY FOLDER "Tests")
set_property(TARGET gtest_main PROPERTY FOLDER "Tests")
