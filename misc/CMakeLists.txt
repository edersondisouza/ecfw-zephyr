zephyr_library()

zephyr_library_include_directories(../app/boards)
zephyr_library_include_directories(../app/boards/microchip)
zephyr_library_include_directories(../app/boards/microchip/mec15xx_mecc)
zephyr_library_include_directories(../app/boards/microchip/mec17xx_mecc)
zephyr_library_include_directories(../app/debug)
zephyr_library_include_directories(../app/kbchost)
zephyr_library_include_directories(../app/peripheral_management)
zephyr_library_include_directories(../app/power_sequencing)
zephyr_library_include_directories(../app/smchost)
zephyr_library_include_directories(../app/thermal_management)

zephyr_include_directories(.)

zephyr_library_sources(
    flashhdr.c
    softstrap.c
    task_handler.c
    )
