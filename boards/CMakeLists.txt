# SPDX-License-Identifier: Apache-2.0

target_sources(app
    PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/board.c
    PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/board.h
    )

if(CONFIG_SOC_FAMILY_MEC)

target_sources_ifdef(CONFIG_BOARD_MEC172X_MTL_S app
    PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/microchip/mtl_s_mec172x.c
    PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/microchip/mtl_s_mec172x.h
    )

target_sources_ifdef(CONFIG_BOARD_MEC172X_PTL_UH app
    PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}/microchip/ptl_uh_mec172x.c
    PUBLIC
    ${CMAKE_CURRENT_LIST_DIR}/microchip/ptl_uh_mec172x.h
    )

target_include_directories(app
    PRIVATE
    ${CMAKE_CURRENT_LIST_DIR}
    ${CMAKE_CURRENT_LIST_DIR}/microchip
    ${CMAKE_CURRENT_LIST_DIR}/microchip/mec15xx_mecc
    ${CMAKE_CURRENT_LIST_DIR}/microchip/mec172x_mecc
    )

endif()
