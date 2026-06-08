if(NOT DEFINED CJSON_LIB_MODE)
    set(CJSON_LIB_MODE "${ACLASS_LIB_MODE}")
endif()

if(NOT DEFINED CJSON_UTILS)
    set(CJSON_UTILS ON)
endif()

if(NOT DEFINED CJSON_NESTING_LIMIT)
    set(CJSON_NESTING_LIMIT 10)
endif()

if(NOT DEFINED CJSON_CIRCULAR_LIMIT)
    set(CJSON_CIRCULAR_LIMIT 10)
endif()

if(NOT DEFINED CJSON_ENABLE_LOCALES)
    set(CJSON_ENABLE_LOCALES OFF)
endif()

set(cjson_src cJSON.c)
set(cjson_inc cJSON.h)

if(CJSON_UTILS)
    list(APPEND cjson_src cJSON_Utils.c)
    list(APPEND cjson_inc cJSON_Utils.h)
endif()

add_library(cjson ${CJSON_LIB_MODE})

target_sources(cjson PRIVATE
    ${cjson_src}
)

target_sources(cjson PUBLIC
    FILE_SET HEADERS
    BASE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}
    FILES     ${cjson_inc}
)

set_target_properties(cjson PROPERTIES
    C_VISIBILITY_PRESET hidden
)

target_compile_definitions(cjson PRIVATE
    CJSON_API_VISIBILITY
    CJSON_NESTING_LIMIT=${CJSON_NESTING_LIMIT}
    CJSON_CIRCULAR_LIMIT=${CJSON_CIRCULAR_LIMIT}
)

if(CJSON_ENABLE_LOCALES)
    target_compile_definitions(cjson PRIVATE
        ENABLE_LOCALES
    )
endif()

if((NOT WIN32) AND (NOT APPLE))
    target_link_libraries(cjson PUBLIC m)
endif()


install(TARGETS cjson
    LIBRARY   DESTINATION lib
    ARCHIVE   DESTINATION lib
    FILE_SET HEADERS DESTINATION include/cjson
)
