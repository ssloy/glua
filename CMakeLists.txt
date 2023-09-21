cmake_minimum_required(VERSION 3.11)
project(glua)

set(CMAKE_CXX_STANDARD 20)

include(FetchContent)
FetchContent_Declare(
        lua
        GIT_REPOSITORY "https://github.com/lua/lua"
        GIT_TAG v5.4.6
        CONFIGURE_COMMAND ""
        BUILD_COMMAND ""
        INSTALL_COMMAND ""
        )

FetchContent_GetProperties(lua)
if(NOT lua_POPULATED)
    FetchContent_Populate(lua)
endif()

SET(SRC_LIBLUA
    ${lua_SOURCE_DIR}/lapi.c
    ${lua_SOURCE_DIR}/lcode.c
    ${lua_SOURCE_DIR}/lctype.c
    ${lua_SOURCE_DIR}/ldebug.c
    ${lua_SOURCE_DIR}/ldo.c
    ${lua_SOURCE_DIR}/ldump.c
    ${lua_SOURCE_DIR}/lfunc.c
    ${lua_SOURCE_DIR}/lgc.c
    ${lua_SOURCE_DIR}/llex.c
    ${lua_SOURCE_DIR}/lmem.c
    ${lua_SOURCE_DIR}/lobject.c
    ${lua_SOURCE_DIR}/lopcodes.c
    ${lua_SOURCE_DIR}/lparser.c
    ${lua_SOURCE_DIR}/lstate.c
    ${lua_SOURCE_DIR}/lstring.c
    ${lua_SOURCE_DIR}/ltable.c
    ${lua_SOURCE_DIR}/ltm.c
    ${lua_SOURCE_DIR}/lundump.c
    ${lua_SOURCE_DIR}/lvm.c
    ${lua_SOURCE_DIR}/lzio.c
    ${lua_SOURCE_DIR}/lauxlib.c
    ${lua_SOURCE_DIR}/lbaselib.c
    ${lua_SOURCE_DIR}/lcorolib.c
    ${lua_SOURCE_DIR}/ldblib.c
    ${lua_SOURCE_DIR}/liolib.c
    ${lua_SOURCE_DIR}/lmathlib.c
    ${lua_SOURCE_DIR}/loadlib.c
    ${lua_SOURCE_DIR}/loslib.c
    ${lua_SOURCE_DIR}/lstrlib.c
    ${lua_SOURCE_DIR}/ltablib.c
    ${lua_SOURCE_DIR}/lutf8lib.c
    ${lua_SOURCE_DIR}/linit.c
)

add_library(lua STATIC ${SRC_LIBLUA})
target_include_directories(lua INTERFACE ${lua_SOURCE_DIR})

file(GLOB SOURCES
        *.h
        *.cpp
    )

add_definitions(-DRESOURCES_DIR=\"${CMAKE_CURRENT_SOURCE_DIR}/\")
add_executable(${PROJECT_NAME} ${SOURCES})
target_link_libraries(${PROJECT_NAME} PRIVATE lua)

