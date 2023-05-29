cmake_minimum_required(VERSION 3.16)

if(CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR)
    message(STATUS "STM32CubeF1 interface loaded as top project")

    project(STM32CubeF1_Project
            LANGUAGES C CXX ASM
            DESCRIPTION "STM32CubeF1 vendor library"
            )

    message(STATUS "STM32CubeF1 - Build is enabled")

    if(HAL)
        add_subdirectory(test/build)
    endif()
endif()

option(HAL "Include HAL" OFF)

message(STATUS "STM32CubeF1 - Check prerequisites")
include(cmake/prerequisites.cmake)

add_library(STM32CubeF1)

target_sources(
    STM32CubeF1
PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_adc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_crc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_dac.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_dma.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_exti.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_fsmc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_gpio.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_i2c.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_pwr.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_rcc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_rtc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_sdmmc.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_spi.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_tim.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_usart.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_usb.c
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Src/stm32f1xx_ll_utils.c
)

target_include_directories(
    STM32CubeF1
PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/STM32F1xx_HAL_Driver/Inc
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/CMSIS/Device/ST/STM32F1xx/Include
    ${CMAKE_CURRENT_SOURCE_DIR}/Drivers/CMSIS/Include
)

target_compile_definitions(
    STM32CubeF1
PUBLIC
    ${MCU}
    USE_FULL_LL_DRIVER
)
