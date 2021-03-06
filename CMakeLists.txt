cmake_minimum_required(VERSION 2.8)
project(project_opal C CXX)
# set(CMAKE_VERBOSE_MAKEFILE "1")

################# PROTO COMPILATION #####################

# location of nanopb top level directory
set(NANOPB_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/nanopb)
# Add the Nanopb directory to this build.
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${NANOPB_DIRS}/extra")
set(NANOPB_SRC_ROOT_FOLDER ${NANOPB_DIRS})
find_package(Nanopb REQUIRED)
include_directories(${NANOPB_INCLUDE_DIRS})

################# FreeRTOS C++ COMPILATION #####################
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/freertos-addons)
if (NOT ${CMAKE_CROSSCOMPILING})
  set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS}
    "-std=c++11 -Wall -Werror -Wextra -Wpedantic -pthread -O0 -g")
endif(NOT ${CMAKE_CROSSCOMPILING})

################# Main COMPILATION #####################
include(${CMAKE_BINARY_DIR}/../extras/CMakeLists.txt)

add_executable(project_opal src/main.cpp)

add_subdirectory("${CMAKE_CURRENT_SOURCE_DIR}/src")

# Define which libraries we want to add here.
target_link_libraries(project_opal freertos shil hecate stabalization)
