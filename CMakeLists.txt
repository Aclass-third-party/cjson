add_library(cjson STATIC
    cJSON.c
    cJSON_Utils.c
)

target_include_directories(cjson PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)

target_link_libraries(cjson PRIVATE m)

install(TARGETS cjson
    LIBRARY   DESTINATION lib
    ARCHIVE   DESTINATION lib
)

install(FILES cJSON.h cJSON_Utils.h DESTINATION include/cjson)
