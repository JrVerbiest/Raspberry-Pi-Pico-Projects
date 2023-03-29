cmake_minimum_required(VERSION 3.12)

include($ENV{PICO_SDK_PATH}/pico_sdk_init.cmake)

project(blink C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

if (PICO_SDK_VERSION_STRING VERSION_LESS "1.3.0")
    message(FATAL_ERROR "Raspberry Pi Pico SDK version 1.3.0 (or later) required. Your version is ${PICO_SDK_VERSION_STRING}")
endif()

pico_sdk_init()

if (TARGET tinyusb_device)
        add_executable(blink
                blink.c
                )

        target_link_libraries(blink pico_stdlib)

        # enable usb output, disable uart output
        pico_enable_stdio_usb(blink 1)
        pico_enable_stdio_uart(blink 0)

        # create map/bin/hex/uf2 file etc.
        pico_add_extra_outputs(blink)

elseif(PICO_ON_DEVICE)
        message(WARNING "not building hello_usb because TinyUSB submodule is not initialized in the SDK")
endif()