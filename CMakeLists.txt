cmake_minimum_required(VERSION 3.13)

project(pico_w_keypad_led C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Pico SDK setup (optional for local builds)
# set(PICO_SDK_PATH "/path/to/pico-sdk")
include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake)

pico_sdk_init()

add_executable(pico_w_keypad_led
  src/main.cpp
)

target_include_directories(pico_w_keypad_led PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}/include
)

# NOTE:
# The firmware uses Arduino APIs and Keypad.h.
# For Pico SDK native builds you must provide compatible wrappers/libraries.

target_link_libraries(pico_w_keypad_led pico_stdlib)

pico_add_extra_outputs(pico_w_keypad_led)
