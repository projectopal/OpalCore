# CMake file for compiling a hecate.
#
# Author: Sam Rosenstein
# Date: 4/16/17
#
# This CMake file follow the example CMake file provided in the examples/module
#   folder.

# At LEAST 3.0 but newer is better.
cmake_minimum_required(VERSION 3.0 FATAL_ERROR)

# Set the module name
set(MODULE_NAME "hecate")
# Set the files needed to compile the module
set(SRCS "hecate.cpp")
# Set if you have a protos folder that is being compiled. Note: This assumes
#   the protos are located under a protos folder.
set(HAS_PROTOS TRUE)
# Set the modules this module requires. All modules require freertos as a base
set(MODULE_REQUIREMENTS "freertos")
# Set the version of the module.
set(MODULE_VERSION "0.1")

opal_module("${MODULE_NAME}" "${MODULE_VERSION}" "${MODULE_REQUIREMENTS}"
            "${SRCS}" "${HAS_PROTOS}")




