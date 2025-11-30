cmake_minimum_required(VERSION 3.12)

project(libuuid VERSION 2.41.2)

option(LIBUUID_BUILD_TEST "build libuuid test" OFF)

include(cmake/precheck.cmake)

set(LIBUUID_SRC_LIST
    ${PROJECT_SOURCE_DIR}/src/clear.c
    ${PROJECT_SOURCE_DIR}/src/copy.c
    ${PROJECT_SOURCE_DIR}/src/gen_uuid.c
    ${PROJECT_SOURCE_DIR}/src/isnull.c
    ${PROJECT_SOURCE_DIR}/src/md5.c
    ${PROJECT_SOURCE_DIR}/src/pack.c
    ${PROJECT_SOURCE_DIR}/src/parse.c
    ${PROJECT_SOURCE_DIR}/src/predefined.c
    ${PROJECT_SOURCE_DIR}/src/randutils.c
    ${PROJECT_SOURCE_DIR}/src/sha1.c
    ${PROJECT_SOURCE_DIR}/src/strutils.c
    ${PROJECT_SOURCE_DIR}/src/timeutils.c
    ${PROJECT_SOURCE_DIR}/src/unpack.c
    ${PROJECT_SOURCE_DIR}/src/unparse.c
    ${PROJECT_SOURCE_DIR}/src/uuid_time.c
)

if(${BUILD_SHARED_LIBS})
    add_library(libuuid SHARED
        ${LIBUUID_SRC_LIST}
    )
else()
    add_library(libuuid STATIC
        ${LIBUUID_SRC_LIST}
    )
endif()

target_compile_definitions(libuuid PRIVATE
    ${ExistHeaderList}
    ${ExistFunctionList}
    ${ExistMacroList}
)

target_include_directories(libuuid
    PUBLIC
        ${PROJECT_SOURCE_DIR}/include
)

if(${LIBUUID_BUILD_TEST})
    add_subdirectory(test)
endif()
