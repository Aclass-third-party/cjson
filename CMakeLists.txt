add_library(cjson STATIC)

target_sources(cjson PRIVATE
    cJSON.c
    cJSON_Utils.c
)

target_sources(cjson PUBLIC
    FILE_SET HEADERS
    BASE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}
    FILES     cJSON.h cJSON_Utils.h
)

target_include_directories(cjson PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
)

target_link_libraries(cjson PRIVATE m)

install(TARGETS cjson
    LIBRARY   DESTINATION lib
    ARCHIVE   DESTINATION lib
    FILE_SET HEADERS DESTINATION include/cjson
)
