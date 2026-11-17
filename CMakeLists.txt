cmake_minimum_required(VERSION 3.25)

project(wetrecomp VERSION 0.1.0 LANGUAGES C CXX)

if(NOT REXGLUE_PLATFORM_SWITCH)
    message(FATAL_ERROR "Configure this project with the ReXGlue Nintendo Switch toolchain.")
endif()

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set(REXSDK_DIR
    "${CMAKE_CURRENT_SOURCE_DIR}/../rexglue-nx-source"
    CACHE PATH "Path to the ReXGlue Nintendo Switch SDK"
)

set(REXGLUE_USE_D3D12 OFF CACHE BOOL "" FORCE)
set(REXGLUE_USE_VULKAN OFF CACHE BOOL "" FORCE)
set(REXGLUE_SWITCH_DEKO3D ON CACHE BOOL "" FORCE)
set(REXGLUE_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(REXGLUE_ENABLE_TRACY OFF CACHE BOOL "" FORCE)
set(REXGLUE_ENABLE_PERF_COUNTERS OFF CACHE BOOL "" FORCE)
set(REXGLUE_ENABLE_FIDELITYFX OFF CACHE BOOL "" FORCE)
set(SPDLOG_NO_TZ_OFFSET ON CACHE BOOL "" FORCE)

include("${CMAKE_CURRENT_SOURCE_DIR}/generated/rexglue.cmake")

add_executable(wetrecomp
    src/main.cpp
    src/game_patches.cpp
    src/render/gpu_wait_hook.cpp
    src/platform/language_hook.cpp
    src/mod/mouse_look/mouse_look.cpp
    src/mod/mouse_look/hook.cpp
)

rexglue_setup_target(wetrecomp)

target_compile_definitions(wetrecomp PRIVATE
    _DEFAULT_SOURCE=1
    _GNU_SOURCE=1
    _POSIX_C_SOURCE=200809L
    SPDLOG_NO_TZ_OFFSET
)

if(TARGET wetrecomp_recomp)
    target_compile_definitions(wetrecomp_recomp PRIVATE
        _DEFAULT_SOURCE=1
        _GNU_SOURCE=1
        _POSIX_C_SOURCE=200809L
        SPDLOG_NO_TZ_OFFSET
    )
endif()

rexglue_switch_add_deko3d(wetrecomp)

rexglue_switch_add_nro(
    wetrecomp
    NAME "WET (X360 Recomp)"
    AUTHOR "PineApple-Geek"
    VERSION "0.1.0"
)
