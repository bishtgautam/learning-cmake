cmake_minimum_required (VERSION 2.8.12)

# For now, we disable shared libs on Macs.
if (APPLE)
  set(BUILD_SHARED_LIBS OFF)
endif()

#if (NOT CMAKE_INSTALL_PREFIX)
#  set(CMAKE_INSTALL_PREFIX /usr/local)
#endif()

# Make sure compilers are set. This must be done before enabling languages.
if (NOT CMAKE_C_COMPILER)
  if (NOT $ENV{CC} STREQUAL "")
    set(CMAKE_C_COMPILER $ENV{CC})
  else()
    set(CMAKE_C_COMPILER cc)
  endif()
endif()
if (NOT CMAKE_C_FLAGS)
  set(CMAKE_C_FLAGS $ENV{CFLAGS})
endif()
if (NOT CMAKE_CXX_COMPILER)
  if (NOT $ENV{CXX} STREQUAL "")
    set(CMAKE_CXX_COMPILER $ENV{CXX})
  else()
    set(CMAKE_CXX_COMPILER c++)
  endif()
endif()
if (NOT CMAKE_CXX_FLAGS)
  set(CMAKE_CXX_FLAGS $ENV{CXX_FLAGS})
endif()
if (NOT CMAKE_Fortran_COMPILER)
  if (NOT $ENV{FC} STREQUAL "")
    set(CMAKE_Fortran_COMPILER $ENV{FC})
  else()
    set(CMAKE_Fortran_COMPILER gfortran)
  endif()
endif()
if (NOT CMAKE_Fortran_FLAGS)
  set(CMAKE_Fortran_FLAGS $ENV{FCFLAGS})
endif()
enable_language(C)
enable_language(CXX)
enable_language(Fortran)

# We declare the project here.
project (HELLOWORLD)

message("-- C compiler is ${CMAKE_C_COMPILER} (${CMAKE_C_COMPILER_ID})")
message("-- CXX compiler is ${CMAKE_CXX_COMPILER} (${CMAKE_CXX_COMPILER_ID})")
message("-- Fortran compiler is ${CMAKE_Fortran_COMPILER} (${CMAKE_Fortran_COMPILER_ID})")

set (HELLOWORLD_VERSION_MAJOR 0)
set (HELLOWORLD_VERSION_MINOR 1)
set (HELLOWORLD_VERSION_PATCH 0)
set (HELLOWORLD_VERSION "${HELLOWORLD_MAJOR_VERSION}.${HELLOWORLD_MINOR_VERSION}.${HELLOWORLD_PATCH_VERSION}")

# Here we make sure CMake-installed binaries use the correct runpath, and 
# that the path is not stripped during installation.
set(CMAKE_INSTALL_RPATH "${CMAKE_INSTALL_PREFIX}/lib")
set(CMAKE_INSTALL_RPATH_USE_LINK_PATH TRUE)

# Other third-party libraries.
#add_subdirectory(3rd-party)

# Include the binary directory in the header file search path,
# since it's where we place the third-party libraries.
#include_directories("${PROJECT_BINARY_DIR}")
#include_directories("${PROJECT_BINARY_DIR}/include")
#link_directories("${PROJECT_BINARY_DIR}/lib")

# Source code itself.
include_directories("${PROJECT_SOURCE_DIR}")
add_subdirectory(src)



