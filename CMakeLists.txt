cmake_minimum_required(VERSION 3.22)

project(NetUMP LANGUAGES C CXX)

add_library(${PROJECT_NAME} STATIC
    # from bbouchez/BEBSDK
    Network.cpp
    SystemSleep.cpp
    # Core netump library
    NetUMP.cpp
    NetUMP_SessionProtocol.cpp
    UMP_Transcoder.c
)

target_include_directories(${PROJECT_NAME}
    PUBLIC
        ${CMAKE_CURRENT_SOURCE_DIR}
)

if(WIN32)
    target_compile_definitions(${PROJECT_NAME}
        PRIVATE
            __TARGET_WIN__=1
    )
elseif(APPLE)
    target_compile_definitions(${PROJECT_NAME}
        PRIVATE
            __TARGET_MAC__=1
    )
elseif(UNIX)
    target_compile_definitions(${PROJECT_NAME}
        PRIVATE
            __TARGET_LINUX__=1
    )
else()
    error("Unsupported platform")
endif()