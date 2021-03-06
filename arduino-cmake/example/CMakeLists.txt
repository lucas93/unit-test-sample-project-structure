# This configuration file outlines some of the ways Arduino CMake
# can be used. For a detailed explenation of all the options please
# reade README.rst.

set(ARDUINO_DEFAULT_BOARD uno) # Default Board ID, when not specified
set(ARDUINO_DEFAULT_PORT /dev/ttyUSB0) # Default Port, when not specified

function(print var_name)
    message(STATUS "${var_name} ===  ${${var_name}}")
endfunction()

#====================================================================#
# master_writer example from Wire library
#====================================================================#
#generate_arduino_example(wire_example
#                         LIBRARY Wire
#                         EXAMPLE master_writer)

# Alternative: by vairables
#set(wire_example_LIBRARY Wire)
#set(wire_example_EXAMPLE master_writer)
#
#generate_arduino_example(wire_example)



#====================================================================#
# Original blink sketch (from Arduino SDK examples)
#====================================================================#

# Some installations have renamed the example directories
#if (EXISTS "${ARDUINO_SDK_PATH}/examples/01.Basics/Blink")
#    set(BLINK_SKETCH "${ARDUINO_SDK_PATH}/examples/01.Basics/Blink")
#else()
#    set(BLINK_SKETCH "${ARDUINO_SDK_PATH}/examples/1.Basics/Blink")
#endif()


#generate_arduino_firmware(blink_original
#    SKETCH "${BLINK_SKETCH}"
#    PORT  /dev/ttyACM0
#    SERIAL picocom @SERIAL_PORT@
#    BOARD uno)

# Alternative: by variables
#set(blink_original_SKETCH "${BLINK_SKETCH}")
#set(blink_original_PORT  /dev/ttyACM)
#set(blink_original_SERIAL picocom @SERIAL_PORT@)
#set(blink_original_BOARD uno)
#
#generate_arduino_firmware(blink_original)




#====================================================================#
# Bundled blink sketch example
#====================================================================#
#generate_arduino_firmware(blink_bundled
#    SKETCH Blink
#    PROGRAMMER usbtinyisp
#    NO_AUTOLIBS)

#include_directories("${ARDUINO_SDK_PATH}/hardware/arduino/cores/arduino")

#message(STATUS "debug ARDUINO_SDK_PATH ===  ${ARDUINO_SDK_PATH}"
# Alternative: by variables
#set(blink_bundled_SKETCH Blink)
#set(blink_bundled_PROGRAMMER usbtinyisp)
#set(blink_bundled_NO_AUTOLIBS true)
#
#generate_arduino_firmware(blink_bundled)




#====================================================================#
# Advanced static library exmaple
#====================================================================#
#generate_arduino_library(blink_lib
#    SRCS blink_lib.cpp
#    HDRS blink_lib.h
#    BOARD uno)

# Alternative: by variables
#set(blink_lib_SRCS blink_lib.cpp)
#set(blink_lib_HDRS blink_lib.h)
#set(blink_lib_BOARD uno)
#
#generate_arduino_library(blink_lib)

set(SOURCES_MAIN_DIRECTORY "${CMAKE_CURRENT_LIST_DIR}/../../application")
print(SOURCES_MAIN_DIRECTORY)

INCLUDE_DIRECTORIES("${SOURCES_MAIN_DIRECTORY}/BaseClass/")

#====================================================================#
# Advanced firwmare example
#====================================================================#
generate_arduino_firmware(blink
    SRCS blink.cpp blink_lib.cpp "/home/lukasz/workspace/test-repo/application/BaseClass/BaseClass.cpp"
    HDRS blink_lib.h "${SOURCES_MAIN_DIRECTORY}/BaseClass/BaseClass.h"
    ARDLIBS SPI Wire
    BOARD uno)


# Alternative: by variables
#set(blink_SRCS blink.cpp)
#set(blink_LIBS blink_lib)
#set(blink_BOARD uno)
#
#generate_arduino_firmware(blink)
