# SPDX-License-Identifier: Apache-2.0

#set(BOARD_ROOT ${CMAKE_CURRENT_LIST_DIR}/out_of_tree_boards)

#include(${CMAKE_CURRENT_LIST_DIR}/boards/CMakeLists.txt)
#include(${CMAKE_CURRENT_LIST_DIR}/drivers/CMakeLists.txt)
#add_subdirectory(drivers)
#include(${CMAKE_CURRENT_LIST_DIR}/misc/CMakeLists.txt)

#Note : The target named "app" is the target name expected by Zephyr RTOS
#include_directories(ecfw_app PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/include)

zephyr_include_directories(include)

add_subdirectory(drivers)
add_subdirectory(misc)
