if (NOT (FREERTOS_PLUS_TCP_NETWORK_IF STREQUAL "ESP32") )
    return()
endif()

if(NOT TARGET esp32_lib)
    message(FATAL_ERROR "For FREERTOS_PLUS_TCP_NETWORK_IF=ESP32 must have a target for the esp32_lib")
endif()
#------------------------------------------------------------------------------
add_library( freertos_plus_tcp_network_if STATIC )

target_sources( freertos_plus_tcp_network_if
  PRIVATE
    NetworkInterface.c
)

target_link_libraries( freertos_plus_tcp_network_if
  PRIVATE
    esp32_lib
)

target_link_libraries( freertos_plus_tcp_network_if
  PUBLIC
    freertos_plus_tcp_port
    freertos_plus_tcp_network_if_common
  PRIVATE
    freertos_kernel
    freertos_plus_tcp
)
