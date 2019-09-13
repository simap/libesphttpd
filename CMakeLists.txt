set (libesphttpd_SOURCES "core/auth.c"
                         "core/httpd-freertos.c"
                         "core/httpd.c"
                         "core/sha1.c"
                         "core/libesphttpd_base64.c"
                         "util/captdns.c"
                         "util/cgiflash.c"
                         "util/cgiredirect.c"
                         "util/cgiwebsocket.c"
                         "util/cgiwifi.c"
                         "util/cgiredirect.c"
                         "util/esp32_flash.c"
                         "util/esp32_httpd_vfs.c"
                         "util/esp32_wifi.c")

if (CONFIG_ESPHTTPD_USE_ESPFS)
    list (APPEND libesphttpd_SOURCES "core/httpd-espfs.c")
endif (CONFIG_ESPHTTPD_USE_ESPFS)

idf_component_register(
    SRCS "${libesphttpd_SOURCES}"
    INCLUDE_DIRS "include"
    PRIV_INCLUDE_DIRS "core"
                      "util"
    REQUIRES "app_update"
             "espfs"
             "json"
             "spi_flash"
             "wpa_supplicant"
)

target_compile_definitions (${COMPONENT_TARGET} PUBLIC -DFREERTOS)