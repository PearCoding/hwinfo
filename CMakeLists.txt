cmake_minimum_required(VERSION 3.1...3.15)

if(${CMAKE_VERSION} VERSION_LESS 3.12)
    cmake_policy(VERSION ${CMAKE_MAJOR_VERSION}.${CMAKE_MINOR_VERSION})
endif()

# Prevent in source builds
if(${CMAKE_SOURCE_DIR} STREQUAL ${CMAKE_BINARY_DIR})
	if(NOT DEFINED WITH_IN_SOURCE_BUILD)
		messag(FATAL_ERROR "CMake generation for hwinfo is not allowed within the source directory! Define WITH_IN_SOURCE_BUILD if absolutely necessary!" )
	endif()
endif()

# Omit superfluous "Up-to-date" messages.
if(NOT DEFINED CMAKE_INSTALL_MESSAGE)
	set(CMAKE_INSTALL_MESSAGE "LAZY")
endif()

# Set default to Release
if (NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE "Release")
endif()

project(hwinfo
	VERSION 1.0
	DESCRIPTION "Hardware Feature Extractor")

add_executable(hwinfo hwinfo.cpp)
target_compile_features(hwinfo PUBLIC cxx_std_17)
install(TARGETS hwinfo)
