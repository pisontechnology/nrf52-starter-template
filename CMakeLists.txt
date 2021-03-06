# Basic CMake configuration
CMAKE_MINIMUM_REQUIRED (VERSION 3.6)
SET(PROJECT_ROOT_DIR_PATH ${CMAKE_CURRENT_SOURCE_DIR})
OPTION(DEFINE_DEBUG "Build the project using debugging code" OFF)

# Configure the GCC toolchain.
INCLUDE(${CMAKE_CURRENT_SOURCE_DIR}/sdk_cmake/configure_armgcc.cmake)

IF(NOT DEFINED FIRMWARE_TARGET)
    message(FATAL_ERROR "FIRMWARE_TARGET NOT DEFINED")
ENDIF()

SET(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/bin/${FIRMWARE_TARGET})
SET(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/bin/${FIRMWARE_TARGET})
PROJECT(nordic_firmware C ASM)

# Configure the Nordic SDK
set(NRF5_SDK_PATH "${CMAKE_CURRENT_SOURCE_DIR}/sdk_nordic")
set(NRF5_VAULT_PATH "${CMAKE_CURRENT_SOURCE_DIR}/vault")
INCLUDE(${CMAKE_CURRENT_SOURCE_DIR}/sdk_cmake/configure_nordic_sdk.cmake)

# Load all the relevant git repository information.
INCLUDE(${CMAKE_CURRENT_SOURCE_DIR}/sdk_cmake/configure_versions.cmake)


# if(NOT DEFINED DEBUG_MODE)
#     MESSAGE(STATUS "DEBUG MODE ENABLED")
#     ADD_DEFINITIONS(-DDEBUG)
# else()
#     MESSAGE(STATUS "DEBUG MODE DISABLED")
# endif()

add_subdirectory(fw-${FIRMWARE_TARGET})
