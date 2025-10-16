# SPDX-License-Identifier: Apache-2.0

target_sources(app
    PRIVATE
    board.c
    PUBLIC
    board.h
    )

if(CONFIG_SOC_FAMILY_MEC)

# RVP + MECC
include(microchip/mec15xx_mecc/CMakeLists.txt)
include(microchip/mec172x_mecc/CMakeLists.txt)

target_sources_ifdef(CONFIG_BOARD_MEC1501_ADL app
    PRIVATE
    microchip/adl_mec1501.c
    PUBLIC
    microchip/adl_mec1501.h
    )

target_sources_ifdef(CONFIG_BOARD_MEC1501_ADL_P app
    PRIVATE
    microchip/adl_p_mec1501.c
    PUBLIC
    microchip/adl_p_mec1501.h
    )

target_sources_ifdef(CONFIG_BOARD_MEC1501_MTL_P app
    PRIVATE
    microchip/mtl_p_mec1501.c
    PUBLIC
    microchip/mtl_p_mec1501.h
    )

target_sources_ifdef(CONFIG_BOARD_MEC172XLJ_MTL_TEMPLATE app
    PRIVATE
    microchip/mtl_template_mec172xlj.c
    PUBLIC
    microchip/mtl_template_mec172xlj.h
    )

target_sources_ifdef(CONFIG_BOARD_MEC172X_MTL_S app
    PRIVATE
    microchip/mtl_s_mec172x.c
    PUBLIC
    microchip/mtl_s_mec172x.h
    )

target_sources_ifdef(CONFIG_BOARD_MEC172X_PTL_UH app
    PRIVATE
    microchip/ptl_uh_mec172x.c
    PUBLIC
    microchip/ptl_uh_mec172x.h
    )

target_include_directories(app
    PRIVATE
    .
    microchip
    microchip/mec15xx_mecc
    microchip/mec172x_mecc
    )

endif()
