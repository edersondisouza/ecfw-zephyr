# SPDX-License-Identifier: Apache-2.0

zephyr_library()

zephyr_library_include_directories(../app/boards)
zephyr_library_include_directories(../app/debug)
zephyr_library_include_directories(../app/smchost)
zephyr_library_include_directories(../app/kbchost)
zephyr_library_include_directories(../app/thermal_management)
zephyr_library_include_directories(../app/power_sequencing)
zephyr_library_include_directories(../app/boards/microchip)
zephyr_library_include_directories(../app/boards/microchip/mec172x_mecc)

zephyr_include_directories(.)

message(WARNING "Building EC common module")

if (CONFIG_PS2_KEYBOARD OR CONFIG_PS2_MOUSE)
zephyr_library_sources(
    ps2kbaux.c
    PUBLIC
    ps2kbaux.h
    )
endif()

zephyr_library_sources_ifdef(CONFIG_KSCAN_EC
    PRIVATE
    kbs_matrix.c
    PUBLIC
    kbs_matrix.h
    kbs_keymap.h
    )

if (CONFIG_KSCAN_EC OR CONFIG_PS2_KEYBOARD)
    if (CONFIG_EC_GTECH_KEYBOARD)
        zephyr_library_sources(
        PRIVATE
        gtech_keymap.c
        )
    endif()
    if (CONFIG_EC_FUJITSU_KEYBOARD)
        zephyr_library_sources(
        PRIVATE
        fujitsu_keymap.c
        )
    endif()
endif()

zephyr_library_sources_ifdef(CONFIG_POSTCODE_MANAGEMENT
    max6958.c
    port80display.c
    )

zephyr_library_sources_ifdef(CONFIG_THERMAL_MANAGEMENT
    adc_sensors.c
    peci_hub.c
    )

zephyr_library_sources(
    eeprom.c
    i2c_hub.c
    espi_hub.c
    espioob_mngr.c
    )

zephyr_library_sources_ifdef(CONFIG_SOC_FAMILY_MEC
    led.c
    )

zephyr_library_sources_ifdef(CONFIG_SOC_SERIES_MEC1501X
    gpio_mec.c
    fan_mec15xx.c
    vci_mec15xx.c
    acpi_mec15xx.c
    )

zephyr_library_sources_ifdef(CONFIG_SOC_SERIES_MEC172X
    gpio_mec.c
    fan_mec15xx.c
    # Require Soc-HW access via device tree
    vci_mec172x.c
    acpi_mec172x.c
    )

add_subdirectory_ifdef(CONFIG_ESPI espi)
add_subdirectory_ifdef(CONFIG_GPIO gpio)
add_subdirectory_ifdef(CONFIG_PECI peci)
