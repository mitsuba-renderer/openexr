cmake_minimum_required (VERSION 2.8)
project(openexr)

# Set a default build configuration (Release)
if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  message(STATUS "Setting build type to 'Release' as none was specified.")
  set(CMAKE_BUILD_TYPE Release CACHE STRING "Choose the type of build." FORCE)
  set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release"
    "MinSizeRel" "RelWithDebInfo")
endif()

if ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wno-switch -Wno-tautological-compare")
endif()

add_subdirectory(IlmBase IlmBase)
include_directories(
  IlmBase/Iex
  IlmBase/Imath
  IlmBase/IlmThread
  IlmBase/Half
  ${CMAKE_CURRENT_BINARY_DIR}/IlmBase/config
)

link_directories(
  ${CMAKE_CURRENT_BINARY_DIR}/IlmBase/Iex
  ${CMAKE_CURRENT_BINARY_DIR}/IlmBase/Imath
  ${CMAKE_CURRENT_BINARY_DIR}/IlmBase/IlmThread
  ${CMAKE_CURRENT_BINARY_DIR}/IlmBase/Half
)

add_subdirectory(OpenEXR OpenEXR)
add_dependencies(IlmImf Iex Imath IlmThread Half)
