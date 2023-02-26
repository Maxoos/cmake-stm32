cmake_minimum_required(VERSION 3.16)

# Setup toolchian
set(CMAKE_C_COMPILER_WORKS 1)
set(CMAKE_CXX_COMPILER_WORKS 1)
set(CMAKE_TOOLCHAIN_FILE ${CMAKE_CURRENT_SOURCE_DIR}/thirdparty/build-tool/cmake/stm32_gcc.cmake)

# set project
project(cmake-stm32 C ASM)

# Set build options
set(USE_HAL 1)


# Setup cubemx directory
set(STM32_CUBE_F4_PATH ${CMAKE_CURRENT_SOURCE_DIR}/BSP)

# Get CMSIS package needed for compilation
find_package(CMSIS COMPONENTS STM32F469NI REQUIRED)

# Set project sources
set(PROJECT_SOURCES
    src/main.c
)

# Set project includes
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

# Include HAL if required else only use CMSIS
if (${USE_HAL})
    message("Building with HAL")
    add_definitions(-DUSE_HAL)
    find_package(HAL COMPONENTS STM32F4 REQUIRED)
    set(LIBRARIES CMSIS::STM32::F469NI HAL::STM32::F4::GPIO)
else()
    message("Building without HAL")
    set(LIBRARIES CMSIS::STM32::F469NI)
endif()

# Set the project executable
add_executable(${PROJECT_NAME} ${PROJECT_SOURCES})

# Link libraries to executable based on HAL or CMSIS
target_link_libraries(${PROJECT_NAME}
 ${LIBRARIES}
 STM32::NoSys
)

# Generated wanted files and printout debug information
stm32_print_size_of_target(${PROJECT_NAME})
stm32_generate_binary_file(${PROJECT_NAME})
stm32_generate_hex_file(${PROJECT_NAME})

# set(CMAKE_C_COMPILER ${CMAKE_CURRENT_SOURCE_DIR}/thirdparty/gcc-arm-none-eabi-7-2018-q2-update/bin/arm-none-eabi-gcc)
# set(CMAKE_CXX_COMPILER ${CMAKE_CURRENT_SOURCE_DIR}/thirdparty/gcc-arm-none-eabi-7-2018-q2-update/bin/arm-none-eabi-g++)
# set(CMAKE_ASM_COMPILER ${CMAKE_CURRENT_SOURCE_DIR}/thirdparty/gcc-arm-none-eabi-7-2018-q2-update/bin/arm-none-eabi-gcc)
