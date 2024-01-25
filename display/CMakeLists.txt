# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.20.0)

# Use the project local board root folder
set(BOARD_ROOT "${CMAKE_CURRENT_SOURCE_DIR}/..")

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(display)

target_sources(app PRIVATE src/main.c)
target_sources(app PRIVATE ${app_sources})
