cmake_minimum_required(VERSION 3.12)

include($ENV{PICO_SDK_PATH}/pico_sdk_init.cmake)
pico_sdk_init()

project(blink)

add_executable(blink
        blink.c
        )

target_link_libraries(blink pico_stdlib)

pico_add_extra_outputs(blink)