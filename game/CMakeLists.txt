# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.20.0)
# Use the project local board root folder
set(BOARD_ROOT "${CMAKE_CURRENT_SOURCE_DIR}/..")
set(DTC_OVERLAY_FILE "${CMAKE_CURRENT_SOURCE_DIR}/../boards/st25dv_lvgl.overlay")

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(lvgl)

FILE(GLOB app_sources src/*.c)
target_sources(app PRIVATE ${app_sources})
