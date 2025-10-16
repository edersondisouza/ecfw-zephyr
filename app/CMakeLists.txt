# SPDX-License-Identifier: Apache-2.0

cmake_minimum_required(VERSION 3.13.1)
find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(ecfw)

zephyr_compile_options(-Werror -Wno-address-of-packed-member)
zephyr_linker_sources(SECTIONS linker/custom-sections.ld)

target_sources(app
    PRIVATE
    app.c
    )

include_directories(boards)
include_directories(peripheral_management)
include_directories(power_sequencing)
include_directories(dnx)
include_directories(power_management)
include_directories(smchost)
include_directories(thermal_management)
include_directories(debug)
include_directories(kbchost)
include_directories(saf)
include_directories(soc_debug_awareness)

#

target_sources_ifdef(CONFIG_PERIPHERAL_MANAGEMENT app
    PRIVATE
    peripheral_management/periphmgmt.c
    peripheral_management/pwrbtnmgmt.c
    PUBLIC
    peripheral_management/periphmgmt.h
    peripheral_management/pwrbtnmgmt.h
    )

target_sources_ifdef(CONFIG_PWRMGMT app
    PRIVATE
    power_sequencing/pwrplane.c
    power_sequencing/dswmode.c
    power_sequencing/deepsx.c
    power_sequencing/pseudog3.c
    power_sequencing/pmc.c
    power_sequencing/pwrseq_utils.c
    PUBLIC
    power_sequencing/pwrplane.h
    power_sequencing/dswmode.h
    power_sequencing/deepsx.h
    power_sequencing/pseudog3.h
    power_sequencing/pmc.h
    power_sequencing/pwrseq_utils.h
    )

target_sources_ifdef(CONFIG_DNX_SUPPORT app
    PRIVATE
    dnx/dnx.c
    PUBLIC
    dnx/dnx.h
    )

target_sources_ifdef(CONFIG_DNX_EC_ASSISTED_TRIGGER app
    PRIVATE
    dnx/dnx_ec_assisted_trigger.c
    PUBLIC
    dnx/dnx_ec_assisted_trigger.h
    )

target_sources_ifdef(CONFIG_SOC_DEBUG_AWARENESS app
    PRIVATE
    soc_debug_awareness/soc_debug.c
    PUBLIC
    soc_debug_awareness/soc_debug.h
    )

target_sources_ifdef(CONFIG_SMCHOST app
    PRIVATE
    smchost/smchost.c
    smchost/smchost_info.c
    smchost/smchost_pm.c
    smchost/smc.c
    smchost/sci.c
    PUBLIC
    smchost/smchost.h
    smchost/smc.h
    smchost/sci.h
    smchost/scicodes.h
    )

target_sources_ifdef(CONFIG_THERMAL_MANAGEMENT app
    PRIVATE
    thermal_management/thermalmgmt.c
    smchost/smchost_thermal.c
    PUBLIC
    thermal_management/thermalmgmt.h
    )

target_sources_ifdef(CONFIG_POSTCODE_MANAGEMENT app
    PRIVATE
    debug/postcodemgmt.c
    PUBLIC
    debug/postcodemgmt.h
    )

target_sources_ifdef(CONFIG_ESPI_PERIPHERAL_8042_KBC app
    PRIVATE
    kbchost/kbchost.c
    kbchost/keyboard_utility.c
    PUBLIC
    kbchost/kbchost.h
    kbchost/keyboard_utility.h
    )

target_sources_ifdef(CONFIG_ESPI_SAF app
    PRIVATE
    saf/saf_config.c
    PUBLIC
    saf/saf_config.h
    )

target_sources_ifdef(CONFIG_SAF_SPI_WINBOND app
    PRIVATE
    saf/saf_spi_winbond.c
    PUBLIC
    saf/saf_spi_winbond.h
    )

add_subdirectory(boards)
