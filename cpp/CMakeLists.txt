cmake_minimum_required (VERSION 3.14.0)
add_compile_options(-Wall)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY lib)

project(libVITA49)

include_directories (include/ src/)

file(GLOB_RECURSE sources CONFIGURE_DEPENDS "src/*.cc")

add_library(libVITA49 SHARED ${sources})
target_include_directories (libVITA49 PUBLIC  ${CMAKE_CURRENT_SOURCE_DIR}/include)

