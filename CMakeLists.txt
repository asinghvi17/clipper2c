cmake_minimum_required(VERSION 3.18)
project(clipper2c LANGUAGES CXX)

set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

add_definitions(-D_HAS_EXCEPTIONS=0) # disable exceptions for STL

option(BUILD_SHARED_LIBS ON)
add_compile_options(-fPIC)

include_directories(vendor/Clipper2/include)
link_directories(vendor/Clipper2/lib)

# C Bindings

file(GLOB_RECURSE SOURCE_FILES  src/*.cpp)

add_library(clipper2c SHARED ${SOURCE_FILES})

target_link_libraries(
  clipper2c
  PRIVATE Clipper2
)

target_include_directories(clipper2c PUBLIC ${PROJECT_SOURCE_DIR}/include)
target_compile_features(clipper2c PRIVATE cxx_std_17)
