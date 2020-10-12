cmake_minimum_required (VERSION 3.14.0)
project(VITA49 VERSION 5.0.0.3)
add_compile_options(-Wall)

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ../bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ../lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ../lib)



set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
#set(Boost_USE_STATIC_LIBS ON)
#find_package(Boost REQUIRED)
#find_path(BOOST_FORMAT_INCLUDE_DIRS "boost/format.hpp" REQUIRED)

include_directories (include/ src/)

file(GLOB_RECURSE sources CONFIGURE_DEPENDS "src/*.cc")
file(GLOB HEADER ${PROJECT_SOURCE_DIR}/include/*.h)

add_library(VITA49 STATIC ${sources})
target_include_directories (VITA49 PUBLIC  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
$<INSTALL_INTERFACE:include/VITA49>)

set_target_properties( VITA49 PROPERTIES PUBLIC_HEADER "${HEADER}" )

include(GNUInstallDirs)
set( version_config "${CMAKE_CURRENT_BINARY_DIR}/VITA49ConfigVersion.cmake" )
include( CMakePackageConfigHelpers )

write_basic_package_version_file( "${version_config}"
    VERSION ${PROJECT_VERSION}
    COMPATIBILITY SameMajorVersion )

install(TARGETS VITA49 EXPORT VITA49Config PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/VITA49 ) 
export( TARGETS VITA49 NAMESPACE VITA49:: FILE VITA49Targets.cmake )

install( EXPORT VITA49Config
  FILE VITA49Targets.cmake
  NAMESPACE VITA49::
  DESTINATION "share/VITA49" )

  install (  FILES VITA49Config.cmake "${version_config}"  DESTINATION "share/VITA49" )
