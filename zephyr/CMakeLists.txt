cmake_minimum_required(VERSION 3.20.0)

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})

# project name
project(mbedtls-original)

file(GLOB mbedtls_sources
  ${ZEPHYR_CURRENT_MODULE_DIR}/library/*.c)

# library name
zephyr_library_named(mbedtls-original)
zephyr_library_sources(PRIVATE
  ${mbedtls_sources})
zephyr_library_include_directories(PUBLIC
  ${ZEPHYR_CURRENT_MODULE_DIR}/include
  ${ZEPHYR_CURRENT_MODULE_DIR}/library)