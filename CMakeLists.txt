cmake_minimum_required(VERSION 3.14) # FetchContent is available in 3.11+, but we'll use 3.14 here

project(TFT_eSPI)

add_compile_options(-Wno-non-c-typedef-for-linkage)
add_compile_options(-Wno-implicit-const-int-float-conversion)

add_compile_definitions(DISABLE_ALL_LIBRARY_WARNINGS)

include(FetchContent)

FetchContent_Declare(
        ArduinoFake
        GIT_REPOSITORY https://github.com/FabioBatSilva/ArduinoFake.git
        GIT_TAG        master
)

FetchContent_MakeAvailable(ArduinoFake)
FetchContent_GetProperties(ArduinoFake)

add_library(${PROJECT_NAME} STATIC
        TFT_eSPI.cpp
)

target_include_directories(${PROJECT_NAME} PRIVATE
        ${ArduinoFake_SOURCE_DIR}/src
        .
        Extensions
)

target_link_libraries(${PROJECT_NAME} PRIVATE ArduinoFake)