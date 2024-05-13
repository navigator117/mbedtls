cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

# project name
project(mbedtls-original)

if(CONFIG_MBEDTLS_ORIGINAL)

# module's dependencies
set(${PROJECT_NAME}_LIBRARIES)

# if compiling current project directly, ZEPHYR_CURRENT_MODULE_DIR must set manually,
# otherwise, current project will be compiled as libraries, ZEPHYR_CURRENT_MODULE_DIR will set automatically
if(CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
  set(ZEPHYR_CURRENT_MODULE_DIR ${CMAKE_CURRENT_SOURCE_DIR})
endif()

file(GLOB ${PROJECT_NAME}_SOURCES
  ${ZEPHYR_CURRENT_MODULE_DIR}/library/*.c)

# library name
if(TARGET ${PROJECT_NAME})
  set(ZEPHYR_CURRENT_LIBRARY ${PROJECT_NAME})
else()
  zephyr_library_named(${PROJECT_NAME})
endif()

zephyr_library_sources(PRIVATE
  ${${PROJECT_NAME}_SOURCES})
zephyr_library_include_directories(PUBLIC
  ${ZEPHYR_CURRENT_MODULE_DIR}/include
  ${ZEPHYR_CURRENT_MODULE_DIR}/library)

zephyr_library_link_libraries(PUBLIC
  ${${PROJECT_NAME}_LIBRARIES})

endif() # CONFIG_MBEDTLS_ORIGINAL