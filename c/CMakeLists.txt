project(yazecminer)

cmake_minimum_required(VERSION 3.0.1)

# enforce C++11
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_CXX_STANDARD 11)

if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
    set(CMAKE_INSTALL_PREFIX "${CMAKE_BINARY_DIR}" CACHE PATH "install prefix" FORCE)
endif(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

# allow user to extent CMAKE_PREFIX_PATH via environment variable
list(APPEND CMAKE_PREFIX_PATH "$ENV{CMAKE_PREFIX_PATH}")

file(GLOB LIB_SRCFILES_C "blake2b-sse/*.c" "jsmn/*.c" "sha256/*.c")

add_library(yazecminer-c
        STATIC
        ${LIB_SRCFILES_C}
        )

set_property(TARGET yazecminer-c PROPERTY C_STANDARD 99)
target_link_libraries(yazecminer-c)

file(GLOB SRCFILES_C "*.c")

add_executable(yazecminer
        ${SRCFILES_C}
        )

target_link_libraries(yazecminer yazecminer-c)